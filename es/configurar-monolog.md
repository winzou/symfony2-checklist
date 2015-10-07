Configurar Monolog
seguridad
El componente que genera los logs de tu aplicación en esencial gestionar tu plataforma web. Symfony implementa el componente Monolog dedicado a esta tarea.

La configuración por defecto está bien para el entorno de desarrollo, pero no es suficiente para el de producción.

 Los cambios a realizar tienen dos objetivos:

* Enviar errores por email al administrador del sitio web (logs de nivel "error");
* Registrar _todas_ las autenticaciones, ya que estos son los logs de nivel "info", que no están registrados por defecto.

Monolog se configura a través del archivo `config_prod.yml`:

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

Listo!

* _Ver [Documentación de Symfony2 Monolog](http://symfony.com/doc/master/cookbook/logging/monolog.html)_
