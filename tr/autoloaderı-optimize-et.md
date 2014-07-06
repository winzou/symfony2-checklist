Autoloaderı (Otomatik Yükleyici) Optimize Et
performans
Varsayılan olarak Composer tam olarak optimize edilmemiş bir autoloader döker. Gerçeği söylemek gerekirse çok fazla sınıfınız varsa autoloader azımsanmayacak kadar çok zaman alır.

Üretim ortamında autoloaderın hızlı olmasını istersiniz. Composer PSR-0 paketlerini sınıf eşlemeye çeviren optimize edilmiş bir autoloader dökebilir, bu da performansı arttırır.

Optimize autoloaderi kullanmak için `dump-autoload` Composer komutuna `--optimize` seçeneğini ekleyin:

    php composer.phar dump-autoload --optimize

Tabii ki bu yöntem komutu biraz uzatır. Varsayılan olarak bu şekilde olmamasının sebebi budur.

* _Bkz. [Composer dump-autoload dokümantasyonu](http://getcomposer.org/doc/03-cli.md#dump-autoload)_
