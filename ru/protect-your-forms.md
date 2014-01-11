Защитить формы
безопасность
Компонент Symfony2 Form автоматически добавляет и валидирует [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) токены за вас.

Убедитесь, что секретный ключ, который используется для генерации токенов, кастомизирован в файле `app/config/parameters.yml`:

    secret:  please_use_a_real_secret_here

Кроме того, токен можно кастомизировать на уровне каждой отдельной формы, что даже лучше. Это можно сделать, добавив опцию `intention` в форме:

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

* _Смотрите также [документацию по Symfony2 Form CSRF защите](http://symfony.com/doc/current/book/forms.html#csrf-protection)_
* _Смотрите также [про CSRF на wikipedia](http://en.wikipedia.org/wiki/Cross-site_request_forgery)_
