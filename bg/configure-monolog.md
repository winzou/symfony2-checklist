Конфигуриране на Monolog
сигурност
Компонентът, генериращ логове на приложението ви, е от важно значение за управление на уеб платформата ви. Symfony2 работи с Monolog, който е посветен на тази задача.

Конфигурацията по подразбиране е добра за средата за разработване, но не достатъчно за продуктовата среда. Промените целят две неща:

* Изпращане на грешките администратора на сайта по имейл (логове с ниво "грешка");
* Дневник с _всички_ автентикации, които са с ниво "info", и не се логват по подразбиране.

Да конфигурираме Monolog във файла  `config_prod.yml`:

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

Това е!

* _Виж [Документация на Symfony2 Monolog](http://symfony.com/doc/master/cookbook/logging/monolog.html)_
