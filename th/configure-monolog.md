กำหนดค่าการทำงานของ Monolog
ความปลอดภัย
การเก็บ log การทำงานของ Application เป็นเรื่องสำคัญอย่างยิ่ง Symfony2 ใช้ Monolog ในการทำหน้าที่นี้

การตั้งค่าพื้นฐานที่มีอยู่แล้วเหมาะสำหรับขั้นตอนในการพัฒนาเท่านั้น แต่ในการใช้งานจริง ​(​Production) ควรมีการตั้งค่าใหม่ ด้วยจุดประสงค์ 2 อย่างคือ:

* ส่งข้อมูลความผิดพลาดของระบบทั้งหมดให้ผู้ดูแลระบบทราบทางอีเมล์ (logs of "error" level)
* บันทึกข้อมูลเมื่อมีการใช้งานระบบความปลอดภัย เช่น การ Login เข้าระบบเป็นต้น (authentications) ซึ่งข้อมูลเหล่านี้โดยค่าพื้นฐานจะเก็บในระดับ info ที่ไม่มีการบันทึกเป็น log ไว้

การตั้งค่า Monolog สามารถจัดการได้ที่ไฟล์ `config_prod.yml`:

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

ประมาณนี้แหละจ้า!

* _See [Symfony2 Monolog documentation](http://symfony.com/doc/master/cookbook/logging/monolog.html)_
