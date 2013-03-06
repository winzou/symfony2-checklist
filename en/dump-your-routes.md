Dump your routes
performance
You can speed up your application by letting Apache handle routes directly, rather than using Symfony2 Router component. There are 2 steps.

### 1. Dump your routes for Apache
Symfony2 embeds a command to dump all your routes in a format understandable by Apache mod_rewrite:

    php app/console router:dump-apache -e=prod --no-debug

And then you can add these rewrite rules in your `web/.htaccess`, or directly in the directory configuration in your `httpd.conf`, it's up to you.

    RewriteEngine On
    # And here the output of the previous command

Of course, be sure to activate the module mod_rewrite in your Apache configuration.

### 2. Tell the router you're using Apache
Now you have to tell Symfony2 that you want to use another Matcher than the default one. Add this to your `config_prod.yml`:

    parameters:
        router.options.matcher.cache_class: ~ # disable router cache
        router.options.matcher_class: Symfony\Component\Routing\Matcher\ApacheUrlMatcher

That's it!

* _See [Symfony2 Apache Router documentation](http://symfony.com/doc/current/cookbook/configuration/apache_router.html)_
* _See [Apache mod_rewrite documentation](http://httpd.apache.org/docs/current/rewrite)_