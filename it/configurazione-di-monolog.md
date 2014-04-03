Configurazione di Monolog
sicurezza
Il componente che genera i log della tua applicazione è essenziale per la gestione della piattaforma web.
Symfony2 dedica il componente Monolog alla gestione di questa task.

La configurazione di default va bene per lo sviluppo, ma non è abbastanza per la produzione.
I cambiamenti da applicare consigliati sono:

* Invio di errori all'amministratore del sito web tramite email (log di livello "error");
* Registrazione di _tutte_ le autenticazioni, dato che questi log sono di livello "info" e quindi non vengono registrati di default.

Configura Monolog all'interno del `config_prod.yml`:

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

Questo è tutto!

* _Vedere la [documentazione del componente Monolog di Symfony2](http://symfony.com/doc/master/cookbook/logging/monolog.html)_
