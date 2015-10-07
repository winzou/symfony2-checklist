Instalar un acelerador PHP
rendimiento
Symfony es un framework flexible y potente...que acaba teniendo un tiempo de ejecución muy lento. Por supuesto, el entorno de producción es mucho más rápido que tu entorno habitual de desarrollo, pero no es suficiente.

Con el fin de de impulsar el rendimiento de la aplicación en producción, es _muy recomendable_ instalar un acelerador PHP como APC.

### En un servidor dedicado

#### En Linux
Para instalar APC en una distribución Linux como Debian, simplemente ejecuta:  

    apt-get install php-apc

Adapta el comando a tu distribución.

#### En Windows
Descomenta la línea correspondiente en tu `php.ini`:

    extension=php_apc.dll

#### En todos los casos
Después de la instalación, hay que activar la extensión. Esto se hace añadiendo esta línea al final de tu archivo `php.ini`:

    [APC]
    apc.enabled=1

### En un hosting compartido
If you are on a shared hosting, you must not have an SSH access. In that case, the best option is to contact the administrator. Say him it's better for its servers to have a PHP Accelerator installed.

  Si estás utilizando un hosting compartido, no debes tener acceso por SSH. En ese caso, la mejor opción es contactar con el administrador. Dile que es mejor para sus servidores que tenga instalado un acelerador PHP.

* _Ver [APC en la documentación de PHP](http://php.net/manual/es/book.apc.php)_
