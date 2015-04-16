ติดตั้ง PHP Accelerator
ประสิทธิภาพ
Symfony2 is a flexible and powerful framework... that ends to a quite slow execution time. Of course, the prod environment is much faster than you usual dev environment, but that's not enough.
Symfony2 มีความยืดหยุ่นและความสามารถสูงมาก แต่ทำท่าว่าจะตกมาตายเพราะเรื่องความเร็ว .... แต่เดี๋ยวก่อน! ทีวีไดเร็ค... เอ้ย คุณต้องไม่เชื่อแน่ๆ ว่าในสภาพแวดล้อมที่ใช้งานจริง (prod environment) มันเร็วมากกว่าขั้นตอนการพัฒนาเยอะมาก แต่นั่นก็ยังไม่ดีพอ

ในขั้นตอนการใช้งานจริงของโปรเจคคุณ _ขอแนะนำอย่างยิ่ง_ ให้คุณติดตั้ง PHP Accelerator เช่น APC ด้วย

### สำหรับเครื่อง dedicated server

#### เครื่อง Linux
การติดตั้ง APC บน linux ตระกูล debian, ใช้คำสั่ง:

    apt-get install php-apc

อาจจะต้องใช้คำสั่งที่ต่างไปแล้วแต่เครื่องที่คุณใช้.

#### เครื่อง Windows
แก้ไขไฟล์ `php.ini` โดยเปิดใช้งานส่วนนี้คือ:

    extension=php_apc.dll

#### ทุกระบบ
หลังจากติดตั้งแล้ว, คุณต้องเปิดใช้งานมันด้วย โดยการเพิ่มบรรทัดตามด้านล่างนี้ในไฟล์ `php.ini`:

    [APC]
    apc.enabled=1

### สำหรับเครื่อง shared hosting
ถ้าคุณใช้งานแชร์โฮส (โอสติ้งที่ใช้งานร่วมกับคนอื่น) คุณไม่สามารถ SSH เข้าเครื่องได้ ในกรณีนั้นก็จะต้องเป็นอะไรที่จำเป็นที่ต้องบอกให้ผู้ดูแลระบบติดตั้งให้ โดยการพยายามพรรณาความดีความงามของการติดตั้ง PHP Accelerator ให้เขารู้ ... ที่สุดแล้วถ้าไม่ได้ ก็.... ;)

* _See [APC on the PHP doc](http://php.net/manual/en/book.apc.php)_
