Protéger vos formulaires
securité
Le composant Form de Symfony2 génère et valide automatiquement un jeton [CSRF](http://fr.wikipedia.org/wiki/Cross-site_request_forgery) pour vous.

Assurez vous juste de bien personnaliser la clé secrête, qui est utilisé pour la génération des jetons, dans votre fichier `app/config/parameters.yml` :

    secret:  utilisez_un_vrai_secret_ici

De plus, vous pouvez rendre unique le jeton pour chaque formulaire, ce qui est encore mieux. Pour cela, définissez l'option `intention` dans vos formulaires :

    namespace Acme\DemoBundle\Form;
	
    use Symfony\Component\OptionsResolver\OptionsResolverInterface;

    class TaskType extends AbstractType
    {
        // ...

        public function setDefaultOptions(OptionsResolverInterface $resolver)
        {
            $resolver->setDefaults(array(
                // Ici, une clé unique par formulaire pour la génération du jeton CSRF
                'intention' => 'task_form',
            ));
        }

        // ...
    }

* _Voir [Protection CSRF des formulaires sur la documentation Symfony2](http://symfony.com/fr/doc/current/book/forms.html#protection-csrf)_
* _Voir [CSRF sur wikipedia](http://fr.wikipedia.org/wiki/Cross-site_request_forgery)_