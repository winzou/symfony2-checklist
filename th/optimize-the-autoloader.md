ปรับจูนระบบ Autoloader
ประสิทธิภาพ
โดยพื้นฐานแล้ว ระบบ autoload ของ Composer ยังไม่ใช่สิ่งที่มีประสิทธิภาพที่สุด เพราะเมื่อคุณมีจำนวนคลาสเยอะมากๆ ระบบ autoload ก็กินเวลาพอสมควร

ใน production environment คุณต้องการให้ระบบ autoload ให้เร็วที่สุด Composer สามารถ dump และเพิ่มประสิทธิภาพในการโหลด ด้วยการรวมคลาสที่เป็นแบบ PSR-0 ไว้ในไฟล์ๆเดียวกันได้ ซึ่งจะทำให้มีประสิทธิภาพดีขั้น

วิธีการทำ เพียงแค่คุณเพิ่มคำสั่ง `--optimize` ต่อท้ายให้กับ `dump-autoload` ของ Composer:

    php composer.phar dump-autoload --optimize

ขั้นตอนนี้อาจใช้เวลาซักหน่อย นั่นเป็นเหตุผลที่มันไม่ได้ทำให้อัตโนมัติตอนติดตั้งโปรเจ็คด้วย Composer คุณต้องทำสิ่งนี้เอง

* _ดูเพิ่มเติม [Composer dump-autoload documentation](http://getcomposer.org/doc/03-cli.md#dump-autoload)_
