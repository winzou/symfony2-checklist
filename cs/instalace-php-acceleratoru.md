Instalace PHP akcelerátoru
Výkon

Symfony2 je flexibilní a robustní framework... což končí pomalým načítáním aplikace. Samozřejmě, produkční prostředí je o hodně rychlejší než to vývojové, ale to pořád nestačí.

Pro zrychlení vaší aplikace v produkčním prostředí je _doporučeno_ nainstalovat PHP akcelerátor, například APC.

### Na dedikovaném serveru

#### Na Linuxu
Pro instalaci APC na debian-based systému použijte příkaz:
    apt-get install php-apc

Nezapomeňte příkaz přizpůsobit vaší distribuci.

#### Na Windows
Odkomentujte daný řádek v souboru `php.ini`:

    extension=php_apc.dll

#### Na všech systémech
Po instalaci musíte provést aktivaci daného rozšíření. To můžete učinit přidáním těchto řádků na konec souboru `php.ini`:

    [APC]
    apc.enabled=1

### Na sdíleném hostingu
Pokud provozujete aplikaci na sdíleném hostingu, nemusíte mít možnost připojit se přes SSH. V tomto případě kontaktujte administrátora hostingu a požádejte jej o instalaci APC.

Další informace:
[APC on the PHP doc](http://php.net/manual/en/book.apc.php)