Utiliser un favicons personnalisé et non celui de base fournit par Symfony2. Vous ne voulez pas que le logo Symfony apparaissent sur le navigateur de vos visiteurs. C'est pourquoi vous devez remplacer l'icône par défaut par le vôtre avant la mise en production.

Vous avez juste à remplacer le fichier : `web/favicon.ico`.

Pour créer un favicons, vous pouvez :

* Utiliser des outils en ligne comme [favicon.cc](http://www.favicon.cc) afin de générer des fichiers `.ico`
* Utiliser une icône PNG. Dans ce cas vous devez définir un `link` dans votre code HTML : `<link rel="icon" type="image/png" href="yourFavIcon.png">`
