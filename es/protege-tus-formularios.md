Protege tus formularios
seguridad

El componente Form de Symfony2 incrusta y valida [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) tokens para ti.
Asegúrate de personalizar tu *secret key*, la cual es utilizada por el generador de token, en tu archivo `app/config/parameters.yml`:

    secret:  please_use_a_real_secret_here

Por otra parte, podrías configurar el token de forma fomulario-por-formulario, que es incluso mejor. Puedes hacerlo definiendo una opción `intention` en tus formularios:

    namespace Acme\DemoBundle\Form;

    use Symfony\Component\OptionsResolver\OptionsResolverInterface;

    class TaskType extends AbstractType
    {
        // ...

        public function setDefaultOptions(OptionsResolverInterface $resolver)
        {
            $resolver->setDefaults(array(
                // a unique key to help generate the secret token
                'intention'  => 'task_form',
            ));
        }

        // ...
    }

* Ver [Docummentación de protección CSRF Symfony2 Form](http://symfony.com/doc/current/book/forms.html#csrf-protection)
* Ver [CSRF en wikipedia](https://es.wikipedia.org/wiki/Cross_Site_Request_Forgery)
