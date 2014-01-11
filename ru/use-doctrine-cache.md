Использовать Doctrine Cache
производительность
В production окружении _крайне рекомендуется_ использовать кэш для Doctrine. Есть два типа кэширования.

### Кэш запросов и метаданных (Query and Metadata Cache)
* Query Cache отвечает за кэширование результата трансфорамции DQL запроса в соответствующий SQL. В production запросы вряд ли будут меняться, поэтому логично их закэшировать.
* Metadata Cache отвечает за кэширование разобранных метаданных из нескольких источников, например: YAML, XML, аннотации и т.п.

Кэширование этой информации включается с помощью следующий параметров в файле `config_prod.yml`:

    doctrine:
        orm:
            auto_mapping: true
            query_cache_driver:    apc
            metadata_cache_driver: apc

### Кэш результатов
Результаты запросов могут быть закэшированы, чтобы не обращаться к базе снова и снова. Так как это более точная настройка, нельзя задать это параметром на все приложение. Можно только задать драйвер:

    doctrine:
        orm:
            auto_mapping: true
            result_cache_driver: apc

Затем необходимо явно указывать использовать кэш или нет во всех важных запросах. Это делается установкой имени и времени жизни для каждого запроса. Посмотреть подробнее можно в [документации по кэшированию результатов Doctrine](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html#result-cache).

### Убедиться, что Doctrine на самом деле использует APC кэш

Задать APC в качестве драйвера кэширования для Doctrine – это отлично. Но проблема в том, что Dependency Injection контейнер генерируется через интерфейс командной строки, и кэш создается так же. И если в `php.ini` не указан параметр `apc.enable_cli = 1`, то DIC будет использовать `FileCacheReader`. Это не то поведение, которое хочется получить.

Чтобы проверить, что APC кэш действительно используется, можно посмотреть в `app/cache/prod/appProdProjectContainer.php`. Он должен содержать следующее:

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
	
Если вы не можете найти `\Doctrine\Common\Cache\ApcCache`, то это значит, что APC не используется.

* _Смотрите также [документацию по Doctrine Cache](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html)_
* _Смотрите также [документацию по конфигурации Doctrine в Symfony2](http://symfony.com/doc/current/reference/configuration/doctrine.html)_
* _Смотрите также пост [Using APC cache with Doctrine and Symfony? Check again!](http://gogs.info/2013/05/using-apc-cache-with-doctrine-symfony)_
