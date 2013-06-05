Utiliser le cache Doctrine
performance
En environnement de production, il est _très recommandé_ d'utiliser le cache Doctrine. Il y a deux types de cache.

### Cache de requête et de metadata
* Le Query Cache met en cache la transformation d'une requête DQL dans sa représentation SQL. En production, vos requêtes ne vont pas changer toutes seules, alors profitons-en pour les mettre en cache.
* Le Metadata Cache met en cache les informations metadata parsées depuis différentes sources, comme YAML, XML, Annotations, etc.

Mettre en cache ces informations se fait en définissant quelques paramètres dans votre fichier de configuration de production `config_prod.yml` :

    doctrine:
        orm:
            auto_mapping: true
                query_cache_driver:    apc
                metadata_cache_driver: apc

### Cache de résultat
Le résultat de vos requêtes peut être mis en cache, afin de ne pas interroger la base de données encore et encore. Comme c'est une mise en place assez fine, il n'y a pas de paramétrage complet pour toute votre application. Vous pouvez juste définir quel pilote utiliser, comme précédemment :

    doctrine:
        orm:
            auto_mapping: true
                result_cache_driver: apc

Mais ensuite, vous devez expliciter comment utiliser ce cache pour toutes vos requêtes sensibles. Cela se fait en définissant un nom et une durée de vie à chacune de vos requêtes cachées. Voir [la documentation Doctrine sur le cache de résultat (en)](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html#result-cache).

* _Voir [documentation Doctrine sur le cache (en)](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html)_
* _Voir [référence Symfony2 sur la configuration](http://symfony.com/fr/doc/current/reference/configuration/doctrine.html)_