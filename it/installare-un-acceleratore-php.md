Installare un acceleratore PHP
prestazioni
Symfony2 è un framework flessibile e potente... che sfocia in un tempo di esecuzione lento. Ovviamente, la modalità di produzione è solitamente molto più veloce della modalità di sviluppo, ma non è ancora abbastanza.

Per accelerare la tua applicazione in produzione, si _raccomanda_ di installare un acceleratore PHP come APC.

### Su un server dedicato

#### Su Linux
Per installare APC su una distribuazione debian-like di linux, lanciare semplicemente da terminale il comando:

    apt-get install php-apc

Adatta il comando alla tua distribuzione.

#### Su Windows
Rimuovere il commento dall'inizio della relativa riga nel tuo `php.ini`:

    extension=php_apc.dll

#### In tutti i casi
Dopo l'installazione, devi attivare l'estensione. Questo viene eseguito aggiungendo questa linea alla fine del tuo `php.ini`:

    [APC]
    apc.enabled=1

### Su un hosting condiviso
Se sei su un hosting condiviso, non dovresti avere un accesso SSH. In quel caso, la migliore opzione è contattare l'amministratore.
Digli che sarebbe meglio per i suoi server avere un acceleratore PHP installato.

* _Vedere la [doucmentazione di APC su php.net](http://php.net/manual/en/book.apc.php)_