Chiave segreta reale
sicurezza
Assicurati che sul server di produzione si stia utilizzando una chiave segreta personalizzata.
Controlla che all'interno del file `app/config/parameters.yml` ci sia:

    secret:  please_use_a_real_secret_here

La chiave segreta di default *non* è veramente segreta, *dovresti* cambiarla con una casuale.
