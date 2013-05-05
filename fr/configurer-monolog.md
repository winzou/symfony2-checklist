Configurer Monolog
sécurité
Le composant générant les logs de votre application sont indispensables pour la gestion de votre plate-forme web. Symfony2 embarque le composant Monolog dédié à cette tâche.

Si la configuration par défaut convient pour l'environnement de développement, elle est un peu légère pour la production. Les modifications à apporter répondent à deux objectifs :

* Envoyer à l'administrateur du site les erreurs par email (logs de niveau "error") ;
* Enregistrer _toutes_ les authentifications, car ce sont des logs de niveaux "info" qui ne sont pas loguées par défaut.

Allons configurer Monolog via le fichier `config_prod.yml` (et non `config.yml` pour ne pas impacter l'environnement de développement) :

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

C'est tout !

* _Voir [Symfony2 Monolog documentation](http://symfony.com/fr/doc/master/cookbook/logging/monolog.html)_
* _Voir [Monolog en production](http://www.kitpages.fr/fr/cms/175/monolog-en-production)_
