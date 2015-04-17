ตรวจสอบ Production Server
พื้นฐาน
เช็คเครื่อง Production Server ก่อนทำการติดตั้งระบบเพื่อใช้งานจริง

คุณมีวิธีตรวจสอบความพร้อมของเครื่อง Server สามวิธีดังนี้:

1. Run คำสั่ง `php app/check.php` เพื่อตรวจเช็คระบบ (คุณต้องสามารถเข้าถึง shell ของเครื่องได้)
2. เรียกไฟล์ `config.php` ผ่านทาง Browser;
3. หรือคุณสามารถตรวจสอบความต้องการของระบบจากเอกสารได้ที่ [documentation reference page](http://symfony.com/doc/current/reference/requirements.html)
