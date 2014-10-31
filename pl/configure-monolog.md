Skonfiguru Monolog
bezpieczeństwo
Komponent  aplikacji  generuący logi (dzienniki zdarzeń) jest  jednym z głownych funkcji pozwalających utrzymać  twoja  aplikację.
W przypadku Symfony 2 tym komponentem jest Monolog.

Domyślna konfiguracja jest poprawna dla  środowiska developerskiego,ale jest niewystarczająca dla produkcyjnego. Aby  to  zmienić  należy zrobić  dwie rzeczy:

* Przesłanie blędów na e-mail administratora (logi z poziomem błędu "error" );
* Zapisywanie wszystkich uwierzytelnień - normalnie uwierzytelnienie ma poziom błędu  "info" , i nie jest domyślnie zapisywane.

Poprawna konfiguracja Monologa powinna znajdować się w pliku  `config_prod.yml` i wyglądać  mniej-więcej tak:

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

I to wszystko!

* _Zobacz [Symfony2 Monolog documentation](http://symfony.com/doc/master/cookbook/logging/monolog.html)_
