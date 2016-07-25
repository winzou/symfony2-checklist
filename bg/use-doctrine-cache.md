Използвайте Doctrine Cache
Скорост
В production среда _силно се препоръчва_ да използвате Doctrine cache. Има два вида кеширане.

### Query и Metadata Cache
* Кеширането на заявките цели кеширане на трансформацията от DQL в SQL еквивалента. В продуктова среда заявките няма да се променят много, така че защо да не ги кеширате.
* Metadata Cache цели кеширането на обработената информация от няколко различни източника, като YAML, XML, Annotations и т.н..

Кеширането се постига чрез настройване на няколко параметъра във вашия production конфигурационен файл  `config_prod.yml`:

    doctrine:
        orm:
            auto_mapping: true
            query_cache_driver:    apc
            metadata_cache_driver: apc

### Result Cache
Резултатът от вашите куерита може да бъде кеширан с цел да не се пращат запитвания към базата данни отново и отново. Понеже това е фина настройка, тя не може да бъде направена глобално. Драйверът се настройва както преди:

    doctrine:
        orm:
            auto_mapping: true
            result_cache_driver: apc

Но после във всички големи куерита изрично трябва да се укаже дали да се използва или не. Вижте [Doctrine Result Cache документацията](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html#result-cache).

### Уверете се, че Doctrine наистина използва вашия APC кеш

Вие конфигурирахте APC като кеширащ драйвер и това е велико. Но проблемът е, че Dependency Injection Container се генерира от интерфейс в командния ред, когато се създава кешът. И ако не нямате  `apc.enable_cli = 1` във вашия `php.ini`, тогава DIC ще използва `FileCacheReader`. Това не е това, което искаме.

За да проверите дали наистина използвате APC кеша, погледнете вашия `app/cache/prod/appProdProjectContainer.php`. Там трябва да има следното:

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
	
Ако не откриете `\Doctrine\Common\Cache\ApcCache`, значи не използвате APC.

* _Виж [Doctrine Cache документация](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html)_
* _Виж [Symfony2 Doctrine справочник на конфигурацията](http://symfony.com/doc/current/reference/configuration/doctrine.html)_
* _Виж [Ползвате APC кеш с Doctrine и Symfony? Проверете отново!](http://gogs.info/2013/05/using-apc-cache-with-doctrine-symfony)_
