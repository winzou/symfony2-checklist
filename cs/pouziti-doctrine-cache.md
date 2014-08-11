Použití Doctrine cache
Výkon
V produkčním prostředí je _doporučeno_ používat cache pro Doctrine. Existují dva typy cache.

### Cache pro dotazy a metadata
* Cache pro dotazy se zaměřuje na cachování přeměny DQL dotazu na základní SQL. V produkci se dotazy vůbec nemění, tak proč je necachovat.
* Cache pro metadata se zaměřuje na cachování získaných metadat z různých zdrojů - například YAML, XML, Anotace, atd.

Cachování těchto informací je možné aktivovat pomocí několika parametrů v konfiguračním souboru `config_prod.yml`:

    doctrine:
        orm:
            auto_mapping: true
            query_cache_driver:    apc
            metadata_cache_driver: apc

### Cache výsledků
Výsledky dotazů mohou být cachovány, aby nebylo nutné posílat stejné dotazy na databázi. Jelikož se jedná o choulostivější úpravu, nemůžete ji provést jednoduchým nastavením parametru. Začněte nstavením ovladače, jako v předchozím bloku:

    doctrine:
        orm:
            auto_mapping: true
            result_cache_driver: apc

Poté musíte zvolit, zda cache použijete nebo nepoužijete pro *veškeré* hlavní dotazy. Toto provedete nastavením názvu a dobu trvání každého cachovaného dotazu. Další informace: [Doctrine Result Cache documentation](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html#result-cache).

### Zajistěte že Doctrine používá APC cache

Nastavili jste APC jako ovladač cache pro Doctrine, to je skvělé. Ale problém je, že kontejner Dependency Injection (DI) je generován pomocí konzoly při sestavení cache. A pokud soubor `php.ini` na vašem serveru neobsahuje řádek `apc.enable_cli = 1`, pak DI kontejner použije cache `FileCacheReader`. A to nechceme.

Pro kontrolu, zda opravdu používáte APC cache, zkontrolujte soubor `app/cache/prod/appProdProjectContainer.php`. Měl by obsahovat toto:

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
	
    Pokud nemůžete najít `\Doctrine\Common\Cache\ApcCache`, pak APC nepoužíváte.

Další informace:
[Doctrine Cache documentation](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html)_
[Symfony2 Doctrine configuration reference](http://symfony.com/doc/current/reference/configuration/doctrine.html)_
[Using APC cache with Doctrine and Symfony? Check again!](http://gogs.info/2013/05/using-apc-cache-with-doctrine-symfony)_
