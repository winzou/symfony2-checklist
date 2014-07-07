Monolog'u ayarla
güvenlik
Web platformunuzun yönetimindeki ana bileşenlerden biri uygulamanızın loglarını oluşturan bileşendir. Symfony2 bu görevi yerine getirmek üzere Monolog ile gelir.

Varsayılan ayarlar geliştirme ortamı için yeterli olmasına rağmen üretim için yeterli değildir. Yapılan değişikliklerin iki amacı vardır:

* Hataları website yöneticisine mail ile gönder ("hata" seviyesindeki loglar);
* "Bilgi" seviyesinde loglar olduğu için varsayılan olarak kaydedilmeyen _tüm_ kimlik doğrulamaları kaydet.

`config_prod.yml` dosyasını kullanarak ayarları yapalım:

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

Bu kadar!

* _Bkz. [Symfony2 Monolog dokümantasyonu](http://symfony.com/doc/master/cookbook/logging/monolog.html)_
