Personalizar páginas de error
base
Si estás habituado a las páginas de error del entorno `dev`, es de esperar que no será el caso de tus futuros visitantes en tu sitio web de producción. Por tanto, debes personalizar las diferentes páginas de error, con la intención de integrarlas en to propio diseño.

Afortunadamente, personalizar páginas de rror es muy fácil. Las vistas están localizadas en el bundle `TwigBundle`, que te da la clave para sobresccribirlas con las tuyas. Las vistas que tienes que crear son `Exception/errorXXX.html.twig`, donde `XXX` es el número del error encontrado. Es altamente recomendable personalizar al menos los errores 404  y 500.

Para utilizar tus propias vistas, hay dos posibles soluciones:

1. Puedes crear un nuevo bundle, que extienda de `TwigBundle`, y añadir tus propias plantillas en el directorio `Resources/views/Exception/errorXXX.html.twig`. Eso te permite utilizarlas en otros proyectos, ya que es un bundle reutilizable.
2. También puede simplemente añadir  tus vistas en el directorio `app/Resources/TwigBundle/views/Exception/errorXXX.html.twig`. Si tus vistas son específicas para el proyeto actual, para evitar tener que crear un bundle sólo para eso.

* Ver [Documentación para personalizar páginas de error en Symfony](http://symfony.com/doc/master/cookbook/controller/error_pages.html)
