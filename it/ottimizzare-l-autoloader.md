Ottimizzare l'autoloader
prestazioni
Di default, Composer fornisce un autoloader che non è completamente ottimizzato.
Per questo, quando hai molte classi, l'autoloader potrebbe prendere del tempo...

Nella modalità di produzione desideri che l'autoloader sia veloce. Composer può estrarre un autoloader ottimizzato che converte le librerie basate su PSR-0 in mappe di classi, che ne migliora le prestazioni.

Per utilizzare l'autoloader ottimizzato, aggiungi semplicemente l'opzione `--optimize` al comando `dump-autoload` di Composer:

    php composer.phar dump-autoload --optimize

Ovviamente, questa opzione rende il tempo di esecuzione del comando un po' più lunga. Per questo non viene eseguito di default.

* _Vedere la [documentazione di Composer delativa al comando dump-autoload](http://getcomposer.org/doc/03-cli.md#dump-autoload)_
