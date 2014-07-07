Formlarını koru
güvenlik
Symfony2 Form bileşeni sizin için otomatik olarak [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) token (bilet) gömer ve doğrular.

`app/config/parameters.yml` dosyanızda bulunan gizli anahtarınızı kişiselleştirdiğinize emin olun, bu anahtar token üretilmesinde kullanılır:

    secret:  please_use_a_real_secret_here

Ayrıca anahtar formdan forma da kişiselleştirilebilir, ki bu daha iyidir. Bunu formlarınızda `intention` seçeneği ile yapabilirsiniz:

    namespace Acme\DemoBundle\Form;
	
    use Symfony\Component\OptionsResolver\OptionsResolverInterface;

    class TaskType extends AbstractType
    {
        // ...

        public function setDefaultOptions(OptionsResolverInterface $resolver)
        {
            $resolver->setDefaults(array(
                // gizli token üretilmesine yardımcı bir tekil anahtar
                'intention'  => 'task_form',
            ));
        }

        // ...
    }

* _Bkz. [Symfony2 Form CSRF engelleme dokümantasyonu](http://symfony.com/doc/current/book/forms.html#csrf-protection)_
* _Bkz. [Wikipedia'da CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery)_
