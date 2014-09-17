Install a PHP Accelerator
performance
Symfony2 is a flexible and powerful framework... that ends to a quite slow execution time. Of course, the prod environment is much faster than you usual dev environment, but that's not enough.

In order to boost your application in production, it is _very recommended_ to install a PHP Accelerator like APC.

### On a dedicated server

#### On Linux
To install APC on a debian-like linux distribution, simply execute:  

    apt-get install php-apc

Adapt the command to your distribution.

#### On Windows
Uncomment the concerned line in your `php.ini`:

    extension=php_apc.dll

#### In all cases
After the installation, you have to activate the extension. This is done by adding this line at the end of your `php.ini`:

    [APC]
    apc.enabled=1

### On a shared hosting
If you are on a shared hosting, you must not have an SSH access. In that case, the best option is to contact the administrator. Say him it's better for its servers to have a PHP Accelerator installed.

* _See [APC on the PHP doc](http://php.net/manual/en/book.apc.php)_