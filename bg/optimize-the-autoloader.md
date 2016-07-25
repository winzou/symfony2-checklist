Оптимизиране на Autoloader
скорост
По подразбиране Composer генерира autoloader, който не е напълно оптимизиран. Наистина, ако имате много класове, autoloader-ът може да отнеме съществено време.

В production среда, autoloader трябва да бъде бърз. Composer може да генерира оптимизиран файл, който конвертира PSR-0 пакетите в такива, classmap, което подобрява изпълнението.

За да използвате оптимизирания autoloader, към Composer командата просто добавете опцията `--optimize` с `dump-autoload`:

    php composer.phar dump-autoload --optimize

Разбира се, удължава размера на командата. Затова не е направена по подразбиране.

* _Виж [Composer dump-autoload документацията](http://getcomposer.org/doc/03-cli.md#dump-autoload)_
