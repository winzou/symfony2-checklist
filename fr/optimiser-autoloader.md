Optimiser l'autoloader
performance

Par défaut, composer génére un autoloader qui n'est pas entièrement optimisé. En effet, lorsque vous avez de nombreuses classes, la génération de l'autoloader peut prendre un temps considérable..

En environnement de production, vous voulez que l'autoloader soit rapide. Composer peut générer un autoloader optimisé qui convertit les arborescences / espace de nom normalisés via PSR-0 en un fichier classmap, améliorant les performances.

Pour utiliser un autoloader optimisé, ajoutez juste l'option `--optimize` à la commande `dump-autoload`.

Commande composer : 

    php composer.phar dump-autoload --optimize

Bien sûr, cette options rend la commande un peu plus longure. C'est pourquoi par défaut elle est désactivée.

* _Voir [Composer dump-autoload documentation](http://getcomposer.org/doc/03-cli.md#dump-autoload)_
