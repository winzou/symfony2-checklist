Installer un accélérateur PHP
performance
Symfony2 est un framework flexible et puissant... ce qui évidemment entraîne des temps d'exécution relativement lent. Bien sûr, l'environnement de production est bien plus rapide que l'environnement de développement que vous avez l'habitude d'utiliser, mais ce n'est pas suffisant.

Pour booster les performances de votre application en production, il est _très recommandé_ d'installer un accélérateur PHP comme APC.

### Sur un serveur dédié

#### Sous Linux
Pour installer APC sur une distribution basée sur Debian, exécutez simplement :

    apt-get install php-apc

Adaptez la commande à votre distribution.

#### Sous Windows
Décommentez la ligne concernée dans votre `php.ini` :

    extension=php_apc.dll

#### Dans tous les cas
Après l'installation, vous devez activer l'extension. Cela se fait en ajoutant cette ligne à la fin de votre `php.ini` :

    [APC]
    apc.enabled=1

### Sur un hébergement mutualisé
Si vous êtes en hébergement mutualisé, vous n'avez certainement pas d'accès SSH. Dans ce cas, la meilleure solution est de contacter votre administrateur. Dites-lui qu'un accélérateur PHP est bon pour ses serveurs (car diminue la charge CPU).

* _Voir [APC on the PHP doc](http://php.net/manual/fr/book.apc.php)_
