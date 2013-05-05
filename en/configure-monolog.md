Configure Monolog
security
The component generating the logs of your application is essential for managing your web platform. Symfony2 ships Monolog component dedicated to this task.

The default configuration is OK for the development environment, but it isn't enough for production. The changes to do deal with two aims:

* Send errors to the website administrator by email (logs of "error" level);
* Record _all_ authentications, as these are logs of "info" level, that are not logged by default.

Let's ocnfigure Monolog thanks to `config_prod.yml`:

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

That's it!

* _See [Symfony2 Monolog documentation](http://symfony.com/doc/master/cookbook/logging/monolog.html)_
