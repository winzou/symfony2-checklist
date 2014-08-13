Optimalizace Autoloaderu
Výkon
Ve výchozím stavu používá Composer autoloader, který není plně optimalizován. Pokud používáte velké množství PHP tříd, autoloader může spotřebovat mnoho času při načítání aplikace...

V produkčním prostředí potřebujete, aby byl autoloader rychlý. Composer může použít optimalizovaný autoloader, který převede balíčky typu PSR-0 na classmap, což zlepší výkon. 

Pro použití optimalizovaného autoloaderu jednoduše přidejte možnost `--optimize` k příkazu `dump-autoload`:

    php composer.phar dump-autoload --optimize

Samozřejmě tato možnost příkaz prodlouží. To je důvod, proč není používána ve výchozím nastavení.

Další informace:
[Composer dump-autoload documentation](http://getcomposer.org/doc/03-cli.md#dump-autoload)_
