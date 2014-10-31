Chroń swoje formularze
bezpieczeństwo
Symfony2 Form Component automatycznie załącza i sprawdza tokeny [CSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery) .

Upewnij się  iż zmieniłeś domyślny klucz, który jest używany przy tworzeniu tokenów.Znajduje się on w  pliku  `app/config/parameters.yml` :

    secret:  please_use_a_real_secret_here


* _Zobacz [Symfony2 Form CSRF protection documentation](http://symfony.com/doc/current/book/forms.html#csrf-protection)_
* _Zobacz [CSRF on wikipedia](http://en.wikipedia.org/wiki/Cross-site_request_forgery)_
