Proteja seus formul‡rios
segurana
Symfony2 Form Component automaticamente incorpora e valida [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) tokens para voc.

Esteja seguro que voc personalizou a sua chave segura, ela Ž utilizada na gera‹o do token seguro, est‡ no arquivo `app/config/parameters.yml`:

    secret:  por_favor_utilize_uma_chave_real_aqui

AlŽm disso, voc pode customizar o token formul‡rio a formul‡rio, o que Ž ainda melhor. Voc pode fazer isso atr‡ves da defini‹o da op‹o `intention` em seus formul‡rios:

    namespace Acme\DemoBundle\Form;

    use Symfony\Component\OptionsResolver\OptionsResolverInterface;

    class TaskType extends AbstractType
    {
        // ...

        public function setDefaultOptions(OptionsResolverInterface $resolver)
        {
            $resolver->setDefaults(array(
                // uma chave unica ajuda a gerar um token secreto
                'intention'  => 'task_form',
            ));
        }

        // ...
    }

* _Veja [Symfony2 Form CSRF protection documentation](http://symfony.com/doc/current/book/forms.html#csrf-protection)_
* _Veja [CSRF na wikipedia](http://pt.wikipedia.org/wiki/Cross-site_request_forgery)_