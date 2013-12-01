Configure o Monolog
segurança
O componente para geração de `logs` da sua aplicação é essencial para gerenciar a sua plataforma web. Symfony2 possue o componente Monolog exclusivamente para essa tarefa.

A configuração padrão está preparada para o ambiente de desenvolvimento, o que não é suficiente para a produção. As mudanças serão realizadas com dois objetivos:

* Enviar os erros para o administrador via e-mail(logs de nível "error")

* Salvar _todas_ as autenticações, como estes são logs de nível "info", eles não são salvos por padrão.

Vamos configurar o Monolog através do arquivo `config_prod.yml`:

    monolog:
        handlers:
            main:
                type:               fingers_crossed
                action_level:       error
                handler:            grouped
            grouped:
                type:               group
                members:            [streamed, swift]
            streamed:
                type:               stream
                path:               "%kernel.logs_dir%/%kernel.environment%.log"
                level:              debug
            swift:
                type:               swift_mailer
                from_email:         FQN@foo.com
                to_email:           webmaster@company.com
                subject:            "OOps"
                level:              debug
            login:
                type:               stream
                path:               "%kernel.logs_dir%/auth.log"
                level:              info
                channels:           security

Isso é tudo!

* _Veja [A documentação do Symfony2 Monolog](http://symfony.com/doc/master/cookbook/logging/monolog.html)_
