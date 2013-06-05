Use Doctrine Cache
performance
In production environment, it is _highly recommanded_ to use Doctrine cache. There are two types of cache.

### Query and Metadata Cache
* The Query Cache aims at caching the transformation of a DQL query to its SQL counterpart. In production, your requests won't change a bit so why not caching them.
* The Metadata Cache aims at caching the parsed metadata from a few different sources like YAML, XML, Annotations, etc.

Caching these information is done by setting a few parameters in your production configuration file `config_prod.yml`:

    doctrine:
        orm:
            auto_mapping: true
                query_cache_driver:    apc
                metadata_cache_driver: apc

### Result Cache
The result of your queries can be cached in order not to query the database again and again. As this is a finer tuning, you can't parameter it application-wide. You can only set the driver as previously:

    doctrine:
        orm:
            auto_mapping: true
                result_cache_driver: apc

But then you have to explicitly use or not use this cache in all your majors queries. This is done by setting the name and lifetime of each query cache. See [Doctrine Result Cache documentation](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html#result-cache).

### Ensure that Doctrine is actually using your APC cache

You configured APC as a cache driver for Doctrine, that's great. But the problem is that the Dependency Injection Container is generated through the Command Line Interface, when cache is built from there. And if you do not have `apc.enable_cli = 1` in your `php.ini`, then the DIC will use `FileCacheReader` instead. That's not what we want.

To check if you are really using APC cache, have a look at your `app/cache/prod/appProdProjectContainer.php`. You should see the following:

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
	
If you can't find `\Doctrine\Common\Cache\ApcCache`, then you are not using APC.

* _See [Doctrine Cache documentation](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html)_
* _See [Symfony2 Doctrine configuration reference](http://symfony.com/doc/current/reference/configuration/doctrine.html)_
* _See [Using APC cache with Doctrine and Symfony? Check again!](http://gogs.info/2013/05/using-apc-cache-with-doctrine-symfony)_
