# JDO #
App Engine používá nejčastěji pro ukládání dat [JDO](http://en.wikipedia.org/wiki/Java_Data_Objects)

Při použití JDO, musí každá entita mít svůj klíč.

## jdoconfig.xml ##
Pro nastavení se používá xml soubor `jdoconfig.xml`.
Příklad takového souboru:
```
<?xml version="1.0" encoding="utf-8"?>
<jdoconfig xmlns="http://java.sun.com/xml/ns/jdo/jdoconfig"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="http://java.sun.com/xml/ns/jdo/jdoconfig">

    <persistence-manager-factory name="transactions-optional">
        <property name="javax.jdo.PersistenceManagerFactoryClass"  value="org.datanucleus.store.appengine.jdo.DatastoreJDOPersistenceManagerFactory"/>
        <property name="javax.jdo.option.ConnectionURL" value="appengine"/>
        <property name="javax.jdo.option.NontransactionalRead" value="true"/>
        <property name="javax.jdo.option.NontransactionalWrite" value="true"/>
        <property name="javax.jdo.option.RetainValues" value="true"/>
        <property name="datanucleus.appengine.autoCreateDatastoreTxns" value="true"/>
    </persistence-manager-factory>
</jdoconfig>
```
Více o [konfiguraci JDO](http://code.google.com/appengine/docs/java/datastore/usingjdo.html#Setting_Up_JDO).

## Persistence Manager Factory ##
Persistence Manager Factory je třída pro získání instance Persistence Manageru podle konfigurace.
Parametr metody `getPersistenceManagerFactory` je jméno definované u elementu `<persistence-manager-factory>` v souboru `jdoconfig.xml`.

```
public final class PMF {
    private static final PersistenceManagerFactory pmfInstance =
        JDOHelper.getPersistenceManagerFactory("transactions-optional");

    private PMF() {}

    public static PersistenceManager get() {
        return pmfInstance.getPersistenceManager();
    }
}
```
Získání instance:
```
    PersistenceManager pm = PMF.get();
```