Zainstaluj akcelerator PHP
wydajność
Symfony2 jest elastycznym i potężnym frameworkim ... przez co do  najszybszych nie należy. Oczywiście  środowisko produkcyjne jest dużo bardziej szybsze niż developerskie, ale czasami to nie wystarcza. 

Aby przyspieszyć wersję produkcyjną aplikacji , jest _bardzo zalecane_ ay zainstalować akcelerator PHP , taki jak np. APC

### Na serwerze Dedykowanym (lub VPS ) 

#### Na Linuxie
Aby zainstalować APC na dystrybucji Debian ,  wykonaj polecenie:  

    apt-get install php-apc

Dla  innych dystrybucji to polecenie może być inne

#### Na Window
Odkomentuj następującą linie w pliku konfiguracyjnym PHP t.j.  `php.ini`:

    extension=php_apc.dll

#### We wszystkich przypadkach
Po instalacji, należy  jeszcze uruchomić zainstalowane rozszerzenie. 
Na końcu pliku  `php.ini` dodaj : 

    [APC]
    apc.enabled=1

### Na współdzielonym hostingu 
W większości przypadków na współdzielonym hostingu nie ma dostepu do SSH. W związku z czym z prośbą o instalację APC należy zwrócić się do administratora.

* _Zobacz [APC on the PHP doc](http://php.net/manual/en/book.apc.php)_