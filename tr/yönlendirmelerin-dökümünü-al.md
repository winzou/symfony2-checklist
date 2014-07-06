Yönlendirmelerin (routes) dökümünü al
performans
Symfony2 Router bileşenini kullanmak yerine, yönlendirmeleri Apache'nin direkt işlemesine izin vererek uygulamanızı hızlandırabilirsiniz. 2 Adım vardır.

### 1. Apache için yönlendirmelerin dökümünü alın
Symfony2 Apache mod_rewrite tarafından anlaşılabilecek formatta bütün yönlendirmelerinizin dökümünü alan bir komut içerir:

    php app/console router:dump-apache -e=prod --no-debug

Sonrasında bu yeniden yazma kurallarını `web/.htaccess` içerisine, ya da direkt klasör ayarlarınızın olduğu `httpd.conf` dosyanıza ekleyebilirsiniz, size kalmış.

    RewriteEngine On
    # Buraya önceki komutun çıktısı gelecek

Tabii ki, Apache ayarlarında mod_rewrite modülünün aktif olduğuna emin olun.

### 2. Yönlendiriciye Apache kullandığınızı söyleyin
Şimdi Symfony2'ye varsayılanın yerine farklı bir eşleştirici kullanacağınızı söylemelisiniz. Bunu `config_prod.yml` dosyasına ekleyin:

    parameters:
        router.options.matcher.cache_class: ~ # yönlendirici önbelleğini etkisizleştir
        router.options.matcher_class: Symfony\Component\Routing\Matcher\ApacheUrlMatcher

Bu kadar!

* _Bkz. [Symfony2 Apache yönlendirici dokümantasyonu](http://symfony.com/doc/current/cookbook/configuration/apache_router.html)_
* _Bkz. [Apache mod_rewrite dokümantasyonu](http://httpd.apache.org/docs/current/rewrite)_