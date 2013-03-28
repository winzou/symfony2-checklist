Customize suas páginas de erro
básico
Se você usa as páginas de erro em seu ambiente de desenvolvimento, isto não é, felizmente, o que os seus visitantes devem ver em caso de erro no seu ambiente de produção. Então, você deve customizar diferentes páginas de erro, afim de integrar estes ao seu layout.

Felizmente, a customização das páginas de erro é realmente fácil. As "views" são localizadas dentro do componente `TwigBundle`, que lhe dá a possibilidade para substituí-los pelos seus. As páginas que você precisa criar são: `Exception/errorXXX.html.twig`, onde `XXX` é o número do erro ocorrido. É altamente recomendado personalizar ao menos as páginas para os erros 404 e 500.

Para usar as suas próprias páginas, existe duas possibilidades:

1. Você pode criar um novo bundle(componente), que estenderá de `TwigBundle`, e colocar os seus arquivos em `Resources/views/Exception/errorXXX.html.twig`. Isso permite que você possa reutilizá-lo em diferentes projetos, pois é um componente reutilizável;
2. Você também pode adicionar as suas páginas no diretório `app/Resources/TwigBundle/views/Exception/errorXXX.html.twig`. Se as suas páginas de erros são específicas para o seu projeto, isso evita que você crie um novo bundle apenas para isto.

* _Veja [Customize error pages on Symfony documentation](http://symfony.com/doc/master/cookbook/controller/error_pages.html)_