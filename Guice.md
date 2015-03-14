# Google guice #

Google guice je jednoduchý Dependency Injection framework. Jeho použití je jednoduché.
## Instalace ##
Do složky `web/WEB-INF/lib` nahrajte soubory:
  * [javax.inject.jar](http://code.google.com/p/ae-cms/downloads/detail?name=javax.inject.jar)
  * [aopalliance.jar](http://code.google.com/p/ae-cms/downloads/detail?name=aopalliance.jar)
  * [guice-snapshot.jar](http://code.google.com/p/ae-cms/downloads/detail?name=guice-snapshot.jar) (Pro app engine musí být zbuildována nejnovější vereze)

Konfigurace je běžná třída, která dědí od `AbstractModule`, zde nastavíme k rozhraním jejich implementace:
```
public class GuiceModule extends AbstractModule {
    public void configure() {
        bind(EntityDAO.class).to(EntityDAOImpl.class);
    }
}
```
Ve třídě, kde chceme Dependecy Injection použít stačí jen přidat anotaci:
```
    @Inject
    EntityDAO entityDAO;
```
A výslednou třídu se všemi závislostmi získáme následovně:
```
    Injector injector = Guice.createInjector(new GuiceModule());
    EntityService entityService = injector.getInstance(EntityService.class);
```

## Odkazy ##
  * Oficiální dokumentace: http://code.google.com/p/google-guice/wiki/GettingStarted
  * Jednoduchý tutoriál: http://www.javabeat.net/articles/29-introduction-to-google-guice-1.html