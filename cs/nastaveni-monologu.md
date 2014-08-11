Nastavení Monologu
Bezpečnost
Komponenta generující logy vaší aplikace je nezbytná pro údržbu vaší aplikace. Symfony2 používá komponentu Monolog určenou pro tento úkol.

Výchozí konfigurace je dobrá pro vývojové prostředí, ale nestačí pro produkční. Je dobré zaměřit se na dvě změny:

* Odesílat chyby administrátorovi webu emailem (logy stupně "error");
* Zaznamenávat _veškeré_ autentizace. Jelikož jsou tyto záznamy stupně "info", nejsou ve výchozím nastavení zapisovány.

Konfigurace Monologu v souboru `config_prod.yml`:

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

Hotovo"

Další informace:
[Symfony2 Monolog documentation](http://symfony.com/doc/master/cookbook/logging/monolog.html)_
