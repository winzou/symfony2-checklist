Ochrana formulářů
Bezpečnost
Symfony2 komponenta 'Form' automaticky vkládá a kontroluje tokeny [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery).

Nezapomeňte zvolit tajný klíč (secret token) v souboru `app/config/parameters.yml`:

    secret:  please_use_a_real_secret_here

Dále můžete nastavit klíč pro každý formulář, což je ještě lepší řešení. To můžete provést definováním možnosti `intention` ve vašem formuláři:

    namespace Acme\DemoBundle\Form;
	
    use Symfony\Component\OptionsResolver\OptionsResolverInterface;

    class TaskType extends AbstractType
    {
        // ...

        public function setDefaultOptions(OptionsResolverInterface $resolver)
        {
            $resolver->setDefaults(array(
                // unikátní klíč který pomůže vygenerovat secret token
                'intention'  => 'task_form',
            ));
        }

        // ...
    }
    
Další informace:
[Symfony2 Form CSRF protection documentation](http://symfony.com/doc/current/book/forms.html#csrf-protection)_
[CSRF on wikipedia](http://en.wikipedia.org/wiki/Cross-site_request_forgery)_
