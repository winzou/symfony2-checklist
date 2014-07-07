Doctrine Cache Kullan
performans
Üretim ortamında Doctrine cache kullanmanız şiddetle önerilir. İki tip cache vardır.

### Sorgu ve MetaData Cache
* Sorgu cache DQL sorgusunun SQL karşılığını kaydetmeyi hedefler. Üretim ortamında istekler değişmeyeceğinden, neden bunları kaydetmeyesiniz.
* Metadata Cache YAML, XML, Annotation gibi kaynaklardan çözümlenen metadatanın kaydedilmesini hedefler.

Bu verilerin cache edilmesi üretim ayar dosyası `config_prod.yml`de birkaç parametre eklenmesi ile yapılır:

    doctrine:
        orm:
            auto_mapping: true
            query_cache_driver:    apc
            metadata_cache_driver: apc

### Sonuç Cache
Sonuç cache, sorgularınızın sonuçlarının, tekrar tekrar veritabanında sorgu çalıştırmamak için, kaydedilmesidir. Bu bir ince ayar olduğu için bunu uygulama çapında parametrize edilemez. Önceden olduğu gibi sadece sürücüyü belirleyebiliriz:

    doctrine:
        orm:
            auto_mapping: true
            result_cache_driver: apc

Bundan sonra kendiniz her ana sorgunuzda ayrıca kullanır ya da kullanmayabilirsiniz. Bu her sorgu cache'in isim ve yaşam süresi belirlenerek yapılır. Bkz. [Doctrine Sonuç Cache dokümantasyonu](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html#result-cache).

### Doctrine'in APC cache'inizi gerçekten kullandığına emin olun

APC'yi Doctrine'in cache sürücüsü olarak ayarladınız, güzel. Ama problem cache oradan oluşturulurken, Dependency Injection Containerın Komut Satırı Arayüzü aracılığı ile oluşturulmuş olması. Eğer `php.ini`de `apc.enable_cli = 1` yoksa, DIC `FileCacheReader`ı kullanılır. Bu istemeyeceğimiz birşey.

Gerçekten APC cache kullandığınızı kontrol etmek için, `app/cache/prod/appProdProjectContainer.php` dosyasına göz atın. Şunu görmelisiniz:

    protected function getDoctrine_Orm_DefaultEntityManagerService()
    {
        $a = $this->get('annotation_reader');
        $b = new \Doctrine\Common\Cache\ApcCache();
        $b->setNamespace('sf2orm_default_5cdc3404d84577b226d7772ca9818908');
        $c = new \Doctrine\Common\Cache\ApcCache();
        $c->setNamespace('sf2orm_default_5cdc3404d84577b226d7772ca9818908');
		
        // ...
		
        $g = new \Doctrine\ORM\Configuration();
        $g->setMetadataCacheImpl($b);
        $g->setQueryCacheImpl($c);
		
        // ...
    }
	
Eğer `\Doctrine\Common\Cache\ApcCache` kısmını bulamazsanız, APC kullanmıyorsunuz demektir.

* _Bkz. [Doctrine Cache dokümantasyonu](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html)_
* _Bkz. [Symfony2 Doctrine ayar referansı](http://symfony.com/doc/current/reference/configuration/doctrine.html)_
* _Bkz. [Doctrine ve Symfony ile APC cache kullanmak? Tekrar kontrol edin!](http://gogs.info/2013/05/using-apc-cache-with-doctrine-symfony)_
