Optimizar el Autoloader
rendimiento
Por defecto, Composer vuelca un autoloader que no está completamente optimizado. De hecho, cuando tienes muchas clases, el autoloader puede tardar un tiempo considerable.

En el entorno de producción, quieres que el autoloader sea rápido. Composer puede volcar un autoloader optimizado que convierte los paquetes PSR-0 en *ClassMap*, las cuales mejoran el rendimiento.

Para utilizar el autoloader optimizado, sólo tienes que añadir la opción `--optimize` al comando de Composer `dump-autoload`:

    php composer.phar dump-autoload --optimize

Por supuesto, esta opción hace que el comando tarde un poco más. Por eso no se hace de forma predeterminada.
  
* _Ver [Documentación de Composer volcar-autoload](http://getcomposer.org/doc/03-cli.md#dump-autoload)_
