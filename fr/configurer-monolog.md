Le composant générant les logs de votre application sont indispensables pour la gestion de votre plate-forme web. Symfony2 embarque le composant Monolog dédié à cette tâche.

Allons configurer Monolog via le fichier  `config_prod.yml` :


	monolog:
		handlers:
			main:
				type:                 fingers_crossed
				action_level:       error
				handler:            grouped
				channels:           !bomo_files
			grouped:
				type:               group
				members:            [streamed, swift]
			streamed:
				type:               stream
				path:               "%kernel.logs_dir%/%kernel.environment%.log"
				level:              debug
			swift:
				type:               swift_mailer
				from_email:        FQN@foo.com
				to_email:           webmaster@company.com
				subject:            "OOps"
				level:              debug
			login:
				type:               stream
				path:               "%kernel.logs_dir%/auth.log"
				level:              info
				channels:           security
			file:
				type:               fingers_crossed
				action_level:       warning
				handler:            file_stream
				channels:           bomo_files
			file_stream:
				type:               stream
				path:               "%kernel.logs_dir%/files.log"
				level:              debug

C'est tout !

* _Voir [Symfony2 Monolog documentation](http://symfony.com/fr/doc/master/cookbook/logging/monolog.html)_