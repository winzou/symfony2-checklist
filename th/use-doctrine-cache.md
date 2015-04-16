ใช้งาน Doctrine แคช
ประสิทธิภาพ
ใน production environment _ขอแนะนำเป็นอย่างยิ่ง_ ให้ใช้งาน Doctrine cache ซึ่งมีอยู่ 2 แบบ

### Query และ Metadata แคช
* Query แคช ทำหน้าที่ในการเก็บข้อมูลการเปลี่ยนคำสั่ง DQL ไปเป็น SQL ใน production จะไม่ค่อยมีการเปลี่ยนแปลงอะไร นั่นเป็นเหตุผลที่เราควรทำแคชไว้
* ส่วน Metadata แคช ใช้จัดเก็บ metadata จาก YAML, XML, Annotations เป็นต้น

การทำแคชใน production สามารถทำได้ด้วยการปรับค่าคอนฟิกเล็กน้อยในไฟล์ `config_prod.yml`:

    doctrine:
        orm:
            auto_mapping: true
            query_cache_driver:    apc
            metadata_cache_driver: apc

### Result Cache
ผลลัพภ์จากการ queries สามารถทำแคชได้ เพื่อที่จะได้ไม่ต้องติดต่อกับฐานข้อมูลโดยตรงซ้ำแล้วซ้ำอีก นี้เป็นอื่งอย่างหนึ่งที่คุณสามารถกำหนดค่าได้ครั้งเดียวใช้ได้ทุกส่วนใน Application:

    doctrine:
        orm:
            auto_mapping: true
            result_cache_driver: apc

แต่ถ้าคุณไม่ต้องการใช้งานแคชผลลัพภ์นี้ทั้งหมดทั้ง Application คุณก็สามารถทำเฉพาะส่วนได้ ลองดูข้อมูลที่ [Doctrine Result Cache documentation](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html#result-cache).

### ตรวจสอบให้แน่ใจว่า Doctrine ได้ใช้งาน APC แคชอย่างถูกต้องแล้ว

เมื่อคุณทำการกำหนดค่า APC แคชให้กับ Doctrine เสร็จแล้ว ถ้าคุณไม่ได้เปิดใช้งาน `apc.enable_cli = 1` ในไฟล์ `php.ini` ระบบ Dependency Injection Container จะไปใช้งาน `FileCacheReader` แทน ซึ่งนั่นไม่ถูกต้องตามที่เราต้องการ ลองตรวจสอบให้แน่ใจอีกครั้ง

ให้เข้าไปดูที่ไฟล์ `app/cache/prod/appProdProjectContainer.php`. และหาว่ามีข้อมูลตามนี้หรือไม่:

    protected function getDoctrine_Orm_DefaultEntityManagerService()
    {
        $a = $this->get('annotation_reader');
        $b = new \Doctrine\Common\Cache\ApcCache();
        $b->setNamespace('sf2orm_default_5cdc3404d84577b226d7772ca9818908');
        $c = new \Doctrine\Common\Cache\ApcCache();
        $c->setNamespace('sf2orm_default_5cdc3404d84577b226d7772ca9818908');

        // ...

        $g = new \Doctrine\ORM\Configuration();
        $g->setMetadataCacheImpl($b);
        $g->setQueryCacheImpl($c);

        // ...
    }

ถ้าคุณไม่เจอ `\Doctrine\Common\Cache\ApcCache` แปลว่าคุณยังไม่ได้ใช้งาน APC

* _ดูเพิ่มเติม [Doctrine Cache documentation](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/caching.html)_
* _ดูเพิ่มเติม [Symfony2 Doctrine configuration reference](http://symfony.com/doc/current/reference/configuration/doctrine.html)_
* _ดูเพิ่มเติม [Using APC cache with Doctrine and Symfony? Check again!](http://gogs.info/2013/05/using-apc-cache-with-doctrine-symfony)_
