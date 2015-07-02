Zoptymalizuj Autoloader
wydajność
Domyślnie Composer zrzuca(tworzy) autoloadera który nie jest  w pełni zoptymalizowany. W  przypadku gdy używasz większej ilości klas, może to rzutować negatywnie na wydajność...

W środowisku produkcyjnym zależny nam jednak na możliwie zoptymalizowanym autoloaderze. Composer może zrzucić zoptymalizowany autoloader który konwertuje paczki PSR-0 w "mapę klas" - co korzystnie wpływa na wydajność.

Aby użyć zoptymalizowanego autoloader użyj opcji `--optimize` na ` dump-autoload` . Polecenie Composera :

    php composer.phar dump-autoload --optimize

Oczywiście polecenie to wykonuje się  dłużej niż normalnie. Dlatego też nie jest domyślnie wykonywane.

* _Zobacz [Composer dump-autoload documentation](http://getcomposer.org/doc/03-cli.md#dump-autoload)_
