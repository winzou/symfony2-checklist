Utilizar la cache de Doctrine
rendimiento
En el entorno de producción, es _altamente recomendable_ utilizar la cache de Doctrine. Hay dos tipos de cache.

### Cache de consulta y metadatos

* La cache de consulta tiene como objetivo el almacenamiento en cache de la transformación de una consulta DQL en contrapartida a SQL. En producción, tus peticiones no cambiarán ni un ápice así que, ¿por qué no cachearlas?

* La cache de metadatos tiene como objetivo el almacenamiento en cache de metadatos analizados desde diferentes fuentes como YAML, XML, Anotaciones, etc.

Se puede cachear esta información estableciendo algunos parámetros en tu archivo de configuración de producción `config_prod.yml`:

    doctrine:
        orm:
            auto_mapping: true
            query_cache_driver:    apc
            metadata_cache_driver: apc

### Cache de resultado

El resultado de tus consultas puede ser cacheado para no hacer peticiones a la base de datos una y otra vez.

Como se trata de una puesta a punto más fina, no se puede parametrizar toda la aplicación. Sólo puedes configurar el conductor como en el caso anterior:

    doctrine:
        orm:
            auto_mapping: true
            result_cache_driver: apc

Pero de esta forma, tienes que utilizar de manera explícita o no esta cache en todas las consultas mayores. Esto se hace configurando el nombre y tiempo de vida de cada consulta de cache. Ver [Documentación del resultado de la Cache de Doctrine ](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html#result-cache).

### Asegurarse de que Doctrine realmente está utilizando la cache APC

Ya tienes configurado APC como conductor de la cache de Doctrine, genial. Pero el problema es que el Contenedor de Inyección de Dependencias se genera a través de la Interfaz de Línea de Comandos, cuando la cache, se va a construir a partir de ahí. Y si no tienes `apc.enable_cli = 1` en tu `php.ini`, el Contenedor de Inyección de Dependencias utilizará `FileCacheReader` en su lugar. Eso no es lo que queremos.

Para comprobar que realmente estás utilizando APC cache, tienes que mirar en tu `app/cache/prod/appProdProjectContainer.php`. Deberías ver lo siguiente:

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

Si no puedes encontrar `\Doctrine\Common\Cache\ApcCache`, entonces es que no estás utilizando APC.

* _Ver [Documentación de Doctrine Cache](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html)_
* _Ver [Symfony2 Doctrine configuration reference](http://symfony.com/doc/current/reference/configuration/doctrine.html)_
* _Ver [Estás utilizando APC cache con Doctrine y Symfony? Compruébalo otra vez](http://gogs.info/2013/05/using-apc-cache-with-doctrine-symfony)_
