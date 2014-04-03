Proteggere i form
sicurezza
Il componente Form di Symfony2 include e convalida automaticamente i token [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) per te.

Assicurati di personalizzare la tua chiave segreta, che viene utilizzata per la generazione dei token, nel file`app/config/parameters.yml`:

    secret:  please_use_a_real_secret_here

Inoltre, potresti personalizzare il token in base al form, che è ancora meglio. Puoi farlo definendo un'opzione `intention` nei tuoi form:

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

* _Vedere la [documentazione di Symfony2 a proposito della protezione dei Form tramite CSRF](http://symfony.com/doc/current/book/forms.html#csrf-protection)_
* _Vedere [CSRF su wikipedia](http://en.wikipedia.org/wiki/Cross-site_request_forgery)_
