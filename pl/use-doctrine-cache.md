Użyj Doctrine Cache
wydajność
W środowisku  produkcyjnym jest _wysoce polecane_ użycie Doctrine cache. Do dyspozycji są dwa typy  cache.

### Cache Zapytań i metadanych
* Cache zapytań służy zapisywaniu w pamięci podręcznej transformacji zapytań DQL na  odpowiadające im zapytania SQL. 
* Cache metadanych służy zapisywaniu w pamięci podręcznej zparsowanych metadanych z kilku rożnych źródeł, takich jak  YAML, XML, Annotacje, itp.

Cacheowanie tych informacji należy uruchomić poprzez zmianę paru parametrów w produkcyjnym pliku konfiguracyjnym `config_prod.yml`:

    doctrine:
        orm:
            auto_mapping: true
            query_cache_driver:    apc
            metadata_cache_driver: apc

### Cache Wyników
Wyniki zapytań mogą być zapisywane w pamięci podręcznej,  po to aby nie odpytywać ciągle bazy danych . Opcji tej  nie można  uruchomić w całej aplikacji. W obrębie całej aplikacji,podobnie jak w poprzednim przykładzie,  ustawiamy tylko konfigurację :

    doctrine:
        orm:
            auto_mapping: true
            result_cache_driver: apc

Natomiast sam decydujesz w którym miejscu aplikacji używasz cacheowania wyników zapytań, użycie tego typu pamięci podręcznej odbywa się poprzez  zdefiniowanie nazwy i długości życia dla każdego zapytania które chcesz cacheować. Zobacz  [Doctrine Result Cache documentation](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html#result-cache).

### Upewnij się że  Doctrine używa  APC

Sama  konfiguracja w config_prod jest prosta,ale czasami niewystarczająca . Problemem jest fakt iż kontener Dependency Injection jest generowany za pomocą linii poleceń . Jeżeli nie masz ustawione `apc.enable_cli = 1` w pliku  `php.ini`, wtedy kontener  DI użyje  `FileCacheReader` Zamiast APC . 

Aby sprawdzić czy twoja aplikacja rzeczywiście używa APC,  zobacz na `app/cache/prod/appProdProjectContainer.php`. Powinieneś zobaczyć : 

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
	
Jeśli nie możesz tam znaleźć  `\Doctrine\Common\Cache\ApcCache`, oznacza to że  APC nie jest używane.

* _Zobacz [Doctrine Cache documentation](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html)_
* _Zobacz [Symfony2 Doctrine configuration reference](http://symfony.com/doc/current/reference/configuration/doctrine.html)_
* _Zobacz [Using APC cache with Doctrine and Symfony? Check again!](http://gogs.info/2013/05/using-apc-cache-with-doctrine-symfony)_
