Exporte suas Rotas para o Apache
performance
Você pode aumentar a velocidade da sua aplicação deixando o Apache manipular sua página diretamente, no lugar de usar o componente Symfony2 Router. Aqui estão os dois passos.

### 1. Exporte suas rotas para o Apache
Symfony2 possui um comando que exporta todas as suas rotas em um formato compreensível pelo modulo mod_rewrite do Apache:

    php app/console router:dump-apache -e=prod --no-debug

E então adicione esses regras de rewrite para o arquivo `web/.htaccess`, ou diretamente no diretório de configuração em seu `httpd.conf`, você quem decide.

    RewriteEngine On
    # E aqui adicione o resultado do comando anterior

E claro, esteja certo que o modulo mod_rewrite está ativo na configuração do Apache.

### 2. Diga para o router que você está usando Apache
Agora você precisa dizer ao Symfony2 que você quer usar outro Matcher que não seja o padrão. Adicione isto ao seu `config_prod.yml`:

    parameters:
        router.options.matcher.cache_class: ~ # disable router cache
        router.options.matcher_class: Symfony\Component\Routing\Matcher\ApacheUrlMatcher

É isso!

* _Veja [Symfony2 Apache Router documentation](http://symfony.com/doc/current/cookbook/configuration/apache_router.html)_
* _Veja [Apache mod_rewrite documentation](http://httpd.apache.org/docs/current/rewrite)_