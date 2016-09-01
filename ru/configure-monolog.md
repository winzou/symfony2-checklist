Сконфигурировать Монолог
безопасность
Компонент, отвечающий за генерацию логов — неотъемлемая часть вашего приложения. В Symfony2 эту задачу выполняет Monolog.

Настройки по-умолчанию подходят для development-окружения, но недостаточны для production-окружения. Необходимые изменения решают две задачи:

* Отправка ошибок администратору сайта по электронной почте (логи с уровнем "error")
* Запись _всех_ аутентификаций, так как по-умолчанию они не логгируются в записях уровня "info"

Сконфигурировать Monolog можно в `config_prod.yml`:

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

И всё готово!

* _[Документация по Symfony2 Monolog ](http://symfony.com/doc/master/cookbook/logging/monolog.html)_
