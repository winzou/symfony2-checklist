Personnaliser les pages d'erreur
basic
Si vous êtes habitués aux pages d'erreur de l'environnement "dev", ce n'est heureusement pas ce que vos visiteurs vont rencontrer en cas d'erreur sur votre site en production. Ainsi, vous devez impérativement personnaliser les différentes pages d'erreur, afin de les intégrer à votre layout. En effet, une page d'erreur hors du temps fera fuir très loin vos visiteurs.

Heureusement, personnaliser les pages d'erreur est quelque chose de très simple. Les vues de ces pages se situent en réalité dans le bundle `TwigBundle`, ce qui vous donne la clé pour les remplacer par les vôtres. Les vues que vous devez créer sont : `Exception/errorXXX.html.twig`, où `XXX` est le numéro de l'erreur rencontrée. Il est fortement conseillé de personnaliser a minima les erreurs 404 et 500.

Pour utiliser vos propres vues il y a deux solutions possibles :

1. Soit vous créez un bundle qui hérite de `TwigBundle` et vous mettez les vues dans le répertoire `Resources/views/Exception/errorXXX.html.twig`. Cela vous permet de les réutiliser dans différents projets car elles sont dans un bundle à part ;
2. Soit vous mettes les vues simplement dans le répertoire `app/Resources/TwigBundle/views/Exception/errorXXX.html.twig`. Si vos vues sont spécifiques au projet en cours, cela vous évite de créer un bundle juste pour cela.

* _Voir [Personnaliser ses pages d'erreur sur la documentation Symfony2](http://symfony.com/fr/doc/current/cookbook/controller/error_pages.html)_
* _Voir [Personnaliser les pages d'erreur sur le cours Symfony2 du siteduzero](http://www.siteduzero.com/informatique/tutoriels/developpez-votre-site-web-avec-le-framework-symfony2/personnaliser-les-pages-d-erreur)_
