Favicon personalizzata
basi
Non si vuole mostrare il logo di Symfony nel browser dei visitatori, per questo, prima di effettuare il deploy, dovresti sostituire la favicon di default con la tua.

Sostituisci il file `web/favicon.ico`.

Per creare delle favicon puoi:

* Utilizzare dei servizi online come [favicon.cc](http://www.favicon.cc) per generare dei file `.ico`;
* Utilizzare un'icona PNG. In quel caso bisogna definire un `link` all'interno dell'HTML: `<link rel="icon" type="image/png" href="yourFavIcon.png">`
