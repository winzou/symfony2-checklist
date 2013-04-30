The component generating the logs of your application are essential for managing your web platform. Symfony2 ships Monolog component dedicated to this task.

Go to do the setting via the file   `config_prod.yml` :


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

That's all !

*_Sight [Symfony2 Monolog documentation](http://symfony.com/fr/doc/master/cookbook/logging/monolog.html)_