Сделать выгрузку роутов
производительность
Приложение можно ускорить, если переложить работу с роутами на Apache вместо использования компонента Symfony2 Router. Это делается в два шага.

### 1. Сделать выгрузку роутов Apache
Symfony2 содержит консольную команду, чтобы выгрузить все роуты приложения в формате, понятном модулю Apache mod_rewrite:

    php app/console router:dump-apache -e=prod --no-debug

Полученную выгрузку можно добавить в `web/.htaccess` или напрямую в конфигурацию директории в `httpd.conf` на выбор.

    RewriteEngine On
    # And here the output of the previous command

Конечно, важно не забыть активировать модуль mod_rewrite в настройках Apache.

### 2. Указать роутеру, что используется Apache
Теперь необходимо указать Symfony2, что используется другой Matcher вместо включенного по умолчанию. Добавьте в `config_prod.yml`:

    parameters:
        router.options.matcher.cache_class: ~ # disable router cache
        router.options.matcher_class: Symfony\Component\Routing\Matcher\ApacheUrlMatcher

И все готово!

* _Смотрите также [документацию по Symfony2 Apache Router](http://symfony.com/doc/current/cookbook/configuration/apache_router.html)_
* _Смотрите также [документацию по Apache mod_rewrite](http://httpd.apache.org/docs/current/rewrite)_