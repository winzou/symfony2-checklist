Utilize o Cache do Doctrine
performance
No ambiente de produção, é _altamente recomendado_ utilizar o cache do Doctrine. Aqui estão dois tipos de cache.

### Query e Metadata Cache
* A Query Cache visa o cacheamento da transformação de DQL query para o SQL. Em produção, as suas requisições não irão mudar, então porque não fazer o cache.
* A Metadata Cache permite o cacheamento das informações de metadata vindas de diferentes formatos como YAML, XML, Annotations, etc.

O cache dessas informações é feito definindo alguns paramêtros no arquivo de configuração `config_prod.yml`:

    doctrine:
        orm:
            auto_mapping: true
                query_cache_driver:    apc
                metadata_cache_driver: apc

### Result Cache
O resultado das suas queries podem ser armazenadas em cache para que a consulta não seja executada no banco de dados várias vezes. Como isso é um ajuste mais delicado, você não consegue apenas alterar um paramêtro em sua aplicação. Você apenas precisa setar o driver como anteriormente:

    doctrine:
        orm:
            auto_mapping: true
                result_cache_driver: apc

Mas você precisa tornar explicito o uso ou não desse cache na maioria de suas queries. Isto é feito setando o nome e o tempo de vida de cada querie. Veja [Doctrine Result Cache documentation](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html#result-cache).

* _Veja [Doctrine Cache documentation](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html)_
* _Veja [Symfony2 Doctrine configuration reference](http://symfony.com/doc/current/reference/configuration/doctrine.html)_