Použití secret tokenu
Bezpečnost
Zajistěte, že produkční serveru používá vhodně zvolený secret token. Kontrolu můžete provést v souboru `app/config/parameters.yml`:

    secret:  please_use_a_real_secret_here

Výchozí token *NENÍ* bezpečný, proto jej *MUSÍTE* nahradit náhodným.
