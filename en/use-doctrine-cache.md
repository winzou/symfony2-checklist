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

* _See [Doctrine Cache documentation](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html)_
* _See [Symfony2 Doctrine configuration reference](http://symfony.com/doc/current/reference/configuration/doctrine.html)_