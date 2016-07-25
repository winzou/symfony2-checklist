Protect your forms
security
Symfony2 Form Component automatically embeds and validate [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) tokens for you.

Be sure to customize your secret key, which is used for the token generation, in your `app/config/parameters.yml` file:

    secret:  please_use_a_real_secret_here

Moreover, you could customize the token on a form-by-form basis, which is even better. You can do that by defining an `intention` option in your forms:

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

* _See [Symfony2 Form CSRF protection documentation](http://symfony.com/doc/current/book/forms.html#csrf-protection)_
* _See [CSRF on wikipedia](http://en.wikipedia.org/wiki/Cross-site_request_forgery)_
