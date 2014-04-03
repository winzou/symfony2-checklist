Utilizzare la cache di Doctrine
prestazioni
In modalità produzione, si _consiglia_ di utilizzare la cache di Doctrine. Ci sono due tipi di cache.

### Cache per query e metadati
* La cache per le query aiuta a mettere in cache la trasformazione di una query DQL nella corrispondente query SQL. In produzione, le tue richieste non cambieranno quindi perché non metterle in cache?
* La cache per i metadati aiuta a mettere in cache i metadati estratti da diverse sorgenti quali YAML, XML, Annotazioni, etc...

Il posizionamento in cache queste informazioni viene fatto impostando alcuni parametri nel file di configurazione della modalità di produzione `config_prod.yml`:

    doctrine:
        orm:
            auto_mapping: true
            query_cache_driver:    apc
            metadata_cache_driver: apc

### Cache dei risultati
Il risultato delle tue query può essere messo in cache per non inviare continue query al database. Dato che si tratta di un raffinamento, non puoi configurarlo per tutta l'applicazione. Puoi solo impostare il driver come fatto precedentemente:

    doctrine:
        orm:
            auto_mapping: true
            result_cache_driver: apc

Ma a questo punto devi esplicitamente utilizzare o non utilizzare questa cache in tutte le grandi query. Questo viene fatto impostando il nome ed il tempo di vita per ogni query in cache. Vedi la [documentazione di Doctrine su caching dei risultati](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html#result-cache).

### Assicurati che Doctrine stia utilizzando la cache APC

Hai configurato APC come driver per la cache per Doctrine, questo è grandioso. Ma il problema è che il container della Dependency Injection è generato attraverso l'interfaccia da linea di comando, quando la cache è generata da lì. E se tu non hai `apc.enable_cli = 1` nel tuo `php.ini`, allora il DIC utilizzerà invece il `FileCacheReader`. E questo non è quello che vogliamo.

Per controllare se stai utilizzando veramente la cache APC, controlla il tuo `app/cache/prod/appProdProjectContainer.php`. Dovresti vedere:

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
	
Se non riesci a trovare `\Doctrine\Common\Cache\ApcCache`, allora non stai utilizzando APC.

* _Vedere la [documentazione sulla cache di Doctrine](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html)_
* _Vedere la parte di [configurazione relativa a Doctrine in Symfony2](http://symfony.com/doc/current/reference/configuration/doctrine.html)_
* _Lettere l'articolo "[Using APC cache with Doctrine and Symfony? Check again!](http://gogs.info/2013/05/using-apc-cache-with-doctrine-symfony)"_
