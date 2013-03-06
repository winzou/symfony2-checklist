Exporter vos routes
performance
Vous pouvez améliorer le temps d'exécution de votre application en laissant Apache s'occuper directement de vos routes, plutôt que d'utiliser le composant Router de Symfony2. Il y a 2 étapes.

### 1. Exporter vos routes pour Apache
Symfony2 embarque une commande pour exporter toutes vos routes dans un format exploitable par le module mod_rewrite d'Apache :

    php app/console router:dump-apache -e=prod --no-debug

Ensuite, vous devez ajouter ces règles de réécritures dans votre `web/.htaccess`, ou directement dans la configuration Apache de votre répertoire (dans `httpd.conf`), à vous de choisir.

    RewriteEngine On
    # Placez ici la sortie de la commande précédente

Bien sûr, assurez-vous d'activer le module mod_rewrite dans votre configuration Apache.

### 2. Dire au routeur qu'on utilise dorénavant Apache
Maintenant, vous devez dire à Symfony2 que vous voulez utiliser un autre Matcher que celui par défaut. Ajoutez ceci à votre `config_prod.yml` :

    parameters:
        router.options.matcher.cache_class: ~ # désactive le cache du routeur
        router.options.matcher_class: Symfony\Component\Routing\Matcher\ApacheUrlMatcher

C'est tout !

* _Voir [Symfony2 Apache Router documentation](http://symfony.com/fr/doc/current/cookbook/configuration/apache_router.html)_
* _Voir [Apache mod_rewrite documentation](http://httpd.apache.org/docs/current/rewrite)_