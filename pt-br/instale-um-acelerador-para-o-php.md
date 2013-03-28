Instale um acelerador para o PHP
performance
Symfony2 é um framework flexível e poderoso... que, obviamente, acaba aumentando relativamente o tempo de execução. É claro que, o ambiente de produção é muito mais rápido que o seu ambiente de desenvolvimento de costume, mas isso não é o suficiente.

Com a intenção de aumentar a velocidade de sua aplicação em produção, é _muito recomendado_ instalar um Acelerador para o PHP como o APC.

### Em um servidor dedicado

#### Plataforma Linux
Para instalar o APC em uma distribuição linux baseada em debian, execute:

    apt-get install php-apc

Adapte o comando para a sua distruição.

#### Plataforma Windows
Descomente a linha a baixo em seu `php.ini`:

    extension=php_apc.dll

#### Em todos os casos
Depois da instalação, você deve habilitar o uso da extensão. Isto é feito adicionando a linha a baixo em seu `php.ini`:

    [APC]
    apc.enabled=1

### Em um host compartilhado
Se você está em um host compartilhado, você pode não ter acesso SSH. Neste caso, a melhor opção é contatar o administrador da sua hospedagem. Diga para ele que é melhor para o seus servidores rodar com um Acelerador PHP.

* _Veja [APC na documentação do PHP](http://php.net/manual/en/book.apc.php)_