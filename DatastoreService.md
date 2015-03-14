# Datastore Service #

Další možností pro práci s daty na App Engine je `DatasoterService`.

## Instance Datastore Service ##
Hlavní třídou pro práci je `DatasotreService`, její instanci získáme takto:
```
    DatastoreService datastore = DatastoreServiceFactory.getDatastoreService();
```

## Práce s entitami ##
Pro ukládání dat se používá třída `Entity`. Ta má dvě důležité metody: `setProperty(String propertyName, Object value)` a `getProperty(String propertyName)`, pomocí nich lze nastavit hodnoty a o práci s entitou stará `DatastoreService`. Třída je deklarována jako `final`, takže ji nelze rozšířit.

Získání konkrétní entity z uložiště podle klíče:
```
    try {
        Entity entity = datastore.get(key);
    } catch (EntityNotFoundException e) {
        ...
    }
```

Získání všech entit:
```
    Query query = new Query("TodoEntity");
    query.addFilter(...);
    List<Entity> entities = datastore.prepare(query).asList(FetchOptions.Builder.withLimit(100));
```

Uložení entity lze provést následujícím způsobem:
```
    datastore.put(entity);
```

Naopak pro smazání je potřeba znát klíč:
```
    datastore.delete(key);
```