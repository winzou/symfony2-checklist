Customize error pages
basis
If you are used to the error pages of the "dev" environment, it is hopefully not the case of your future visitors on your production website. So, you must customize the different error pages, in order to integrate them with your own layout. 

Hopefully, customizing error pages is really easy. Their views are located in the `TwigBundle` bundle, that gives you the key to override them by yours. The views you have to create are: `Exception/errorXXX.html.twig`, where `XXX` is the number of the encountered error. It is highly recommended to customize at least errors 404 and 500.

To use your own views, there are two possible solutions:

1. You can create a new bundle, that extends `TwigBundle`, and put your views in the directory `Resources/views/Exception/errorXXX.html.twig`. That enable you to reuse them in different projects as it is a reusable bundle;
2. You can also simply put your views in the directory `app/Resources/TwigBundle/views/Exception/errorXXX.html.twig`. If your views are specific to the current project, it avoid you to create a new bundle just for that.

* _See [Customize error pages on Symfony documentation](http://symfony.com/doc/master/cookbook/controller/error_pages.html)_