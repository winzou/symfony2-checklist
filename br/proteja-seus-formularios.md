Proteja seus formulários
segurança
Symfony2 Form Component automaticamente incorpora e valida [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) tokens para você.

Esteja seguro que você personalizou a sua chave segura, ela é utilizada na geração do token seguro, está no arquivo `app/config/parameters.yml`:

    secret:  por_favor_utilize_uma_chave_real_aqui

Além disso, você pode customizar o token formulário a formulário, o que é ainda melhor. Você pode fazer isso atráves da definição da opção `intention` em seus formulários:

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