แก้ไขหน้า Error Page ใหม่
พื้นฐาน
ถ้าคุณใช้หน้า Error pages สำหรับ Production อันเดียวกับในขั้นตอนการ Develop นั่นจะเป็นอะไรที่ไม่ดีสำหรับคนใช้งานเว็บของคุณแน่ๆ คุณควรเปลี่ยนหน้า Error pages เหล่านั้นใหม่ เพื่อให้เว็บไซต์ของคุณดูดีขึ้นเวลาที่มี Error

อย่างที่คุณหวังไว้เลย, การปรับแต่งหน้า error pages ง่ายมากๆ หน้าเพจเหล่านั้นเป็นส่วนหนึ่งของ `TwigBundle` แปลว่าเราแค่ Override มันเท่านั้นเอง ไฟล์ที่เราต้องแก้ไขทั้งทั้งหมดถูกเก็บไว้ที่ `Exception/errorXXX.html.twig` โดยที่ `XXX` คือหมายเลข Error ต่างๆ ขอแนะนำเป็นอย่างยิ่งให้คุณแก้ไขหน้า errors 404 and 500

มีวิธีการอยู่ 2 วิธีให้คุณเลือก:

1. สร้าง Bundle ขึ้นมาใหม่โดยทำการ extends `TwigBundle` และสร้างไฟล์เดียวกันไว้ที่ `Resources/views/Exception/errorXXX.html.twig` วิธีการนี้เหมาะมากถ้าคุณต้องการใช้ errors เพจเดียวกันนี้ในโปรเจ็คอื่นๆ ด้วย เพราะแค่ใช้ Bundle นี้ในโปรเจคอื่นเท่านั้นเอง
2. หรือว่าคุณจะเขียนไฟล์เหล่านั้นไว้ที่ `app/Resources/TwigBundle/views/Exception/errorXXX.html.twig` ก็ได้ ถ้าคุณไม่อยากสร้าง Bundle ใหม่
* _See [Customize error pages on Symfony documentation](http://symfony.com/doc/master/cookbook/controller/error_pages.html)_
