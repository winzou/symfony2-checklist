Přizpůsobení chybových stránek
Základy

Možná jste zvyklí na chybové stránky z vývojového prostředí, ale vaši budoucí návštěvníci pravděpodobně nebudou. Proto musíte přizpůsobit chybové stránky pro jejich integraci do vámi použitého vzhledu stránek.

Naštěstí lze chybové stránky přizpůsobit velice snadno. Jejich 'views' jsou umístěny v modulu (bundle) `TwigBundle`, což vám dává možnost přepsat je vašimi. 'Views' které musíte vytvořit jsou: `Exception/errorXXX.html.twig`, kde `XXX` je číselná hodnota chyby. Je doporučeno přizpůsobit alespoň stránky pro chyby 404 a 500.

Pro použití vašich 'views' existují dvě možnosti:

1. Můžete vytvořit nový modul (bundle), který rozšíří `TwigBundle` a umístit 'views' do složky `Resources/views/Exception/errorXXX.html.twig`. To vám umožní znovu použít kód na dalších projektech;
2. Můžete jednoduše přidat vaše 'views' do složky `app/Resources/TwigBundle/views/Exception/errorXXX.html.twig`. Pokud jsou určeny pouze pro daný projekt, vyhnete se tím zbytečnému vytváření nového modulu.

Další informace:
[Customize error pages on Symfony documentation](http://symfony.com/doc/master/cookbook/controller/error_pages.html)_