Personalizzare le pagine di errore
basi
Mentre tu potresti essere abituato alle pagine d'errore della modalità sviluppo, non è il caso invece di mostrare gli errori ai futuri visitatori una volta in produzione. Quindi dovresti personalizzare le diverse pagine d'errore, per integrarle nel tuo layout.

Per fortuna, la personalizzazione delle pagine d'errore è veramente semplice. Le viste sono posizionate nel bundle `TwigBundle`, che ti fornisce la chiave per sovrascrivere con le tue. Le viste che devi creare sono: `Exception/errorXXX.html.twig`, dove `XXX` è il numero dell'errore. Si consiglia i personalizzare almeno gli errori 404 e 500.

Per utilizzare le tue viste, ci sono due possibili soluzioni:

1. Puoi creare un nuovo bundle, che estende `TwigBundle`, e posizione le tue viste nella directory `Resources/views/Exception/errorXXX.html.twig`. Questo ti consente di riutilizzarle in diversi progetti come un bundle riutilizzabile;
2. Puoi semplicemente mettere le tue viste nella directory `app/Resources/TwigBundle/views/Exception/errorXXX.html.twig`. Se le tue viste sono specifiche per il progetto corrente, questo ti evita di creare un bundle solo per quello.

* _Vedere la pagina della [documentazione di Symfony sulla personalizzazione delle pagine d'errore](http://symfony.com/doc/master/cookbook/controller/error_pages.html)_