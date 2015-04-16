ป้องกันฟร์อมของคุณ
ความปลอดภัย
ฟอร์มของ Symfony2 ฝังและตรวจสอบ [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) ให้โดยอัตโมัติ

ตรวจสอบให้แน่ใจว่าคุณเปลี่ยนรหัสลับของโปรเจ็คแล้ว เข้าไปตรวจสอบได้ที่ไฟล์ `app/config/parameters.yml`:

    secret:  please_use_a_real_secret_here

อย่างไรซะ การสร้างโทคเคนใหม่เสมอให้ทุกๆฟอร์มที่คุณใช้ก็จะเป็นเรื่องที่ดีกว่า คุณสามารถทำสิ่งนี้ได้ด้วยการเพิ่มอ๊อปชั่น `intention` ตอนที่คุณสร้างฟอร์ม ดังนี้:

    namespace Acme\DemoBundle\Form;

    use Symfony\Component\OptionsResolver\OptionsResolverInterface;

    class TaskType extends AbstractType
    {
        // ...

        public function setDefaultOptions(OptionsResolverInterface $resolver)
        {
            $resolver->setDefaults(array(
                // unique key สำหรับสร้างรหัสรับใหม่ในแต่ละฟอร์ม
                'intention'  => 'task_form',
            ));
        }

        // ...
    }

* _ดูเพิ่มเติม [Symfony2 Form CSRF protection documentation](http://symfony.com/doc/current/book/forms.html#csrf-protection)_
* _ดูเพิ่มเติม [CSRF on wikipedia](http://en.wikipedia.org/wiki/Cross-site_request_forgery)_
