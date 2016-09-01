Защитете формите си
Сигурност
Компонентът за форми на Symfony2 автоматично добавя и валидира [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) токени.

Уверете се, че сте персонализирали тайния си ключ, който се използва в токен генератора, във вашия  `app/config/parameters.yml` файл:

    secret:  please_use_a_real_secret_here

Освен това, можете да персонализирате токените форма по форма, което е още по-добре. Това става като дефинирате опцията `intention` във формите си:

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

* _Виж [Документация за Symfony2 Form CSRF защита](http://symfony.com/doc/current/book/forms.html#csrf-protection)_
* _Виж [CSRF на уикипедия](http://en.wikipedia.org/wiki/Cross-site_request_forgery)_
