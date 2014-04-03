Persistenza delle rotte
prestazioni
Puoi accelerare l'applciazione permettendo ad Apache di gestire direttamente le rotte, invece di utilizzare il componente Router di Symfony2. Ci sono 2 passaggi.

### 1. Estrazione delle rotte per Apache
Symfony2 include un comando per estrarre tutte le rotte in un formato comprensibile dal mod_rewrite di Apache:

    php app/console router:dump-apache -e=prod --no-debug

Quindi puoi aggiungere queste regole di rewrite al tuo `web/.htaccess`, oppure direttamente nella configurazione della directory nel tuo `httpd.conf`, spetta a te decidere.

    RewriteEngine On
    # Aggiungi qui l'output del precedente comando

Ovviamente, assicurati di attivare il modulo mod_rewrite nella tua configurazione di Apache.

### 2. Dire al router che stai utilizzando Apache
Ora devi dire a Symfony2 che vuoi utilizzare un altro Matcher rispetto a quello di default. Aggiungi questo al tuo `config_prod.yml`:

    parameters:
        router.options.matcher.cache_class: ~ # disable router cache
        router.options.matcher_class: Symfony\Component\Routing\Matcher\ApacheUrlMatcher

Questo è tutto!

* _Vedere la [documentazione la documentazione di Symfony2 relativa al Router per Apache](http://symfony.com/doc/current/cookbook/configuration/apache_router.html)_
* _Vedere la [documentazione di Apache relativa al mod_rewrite](http://httpd.apache.org/docs/current/rewrite)_