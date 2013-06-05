Optimize the Autoloader
performance
By default, Composer dumps an autoloader that isn't fully optimized. Indeed, when you have many classes, the autoloader can take up a substantial time..

In production environment, you want the autoloader to be fast. Composer can dump an optimized autoloader that converts PSR-0 packages into classmap ones, which improves performance.

To use the optimized autoloader, just add the `--optimize` option to the `dump-autoload` Composer command:

    php composer.phar dump-autoload --optimize

Of course, this option makes the command a bit longer. That's why it isn't done by default.

* _See [Composer dump-autoload documentation](http://getcomposer.org/doc/03-cli.md#dump-autoload)_
