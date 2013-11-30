Otimize o autoloader
performance
Por padrão, o Composer gera um autoloader que não é totalmente otimizado.
De fato, quando você possue muitas classes, o autoloader pode tomar um tempo considerável...

No ambiente de produção, você quer que o autoloader seja rápido. O Composer pode gerar um autoloader otimizado, que converte pacotes que utilizam a PSR-0 em um único mapeamento de classes, o que melhora o desempenho.

Para usar o autoloader otimizado, apenas adicione a opção `--optimize` para o comando `dump-autoload` do Composer:

    php composer.phar dump-autoload --optimize

É claro, esta opção faz com que o comando demore um pouco mais. Por isso que ela não vem habilitada por padrão.

* _Veja [Documentação do Composer dump-autoload](http://getcomposer.org/doc/03-cli.md#dump-autoload)_
