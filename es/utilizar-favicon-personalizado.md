Utilizar un Favicon personalizado
base
Seguro que no quieres que el logo de Symfony aparezca en el navegador de tus vistantes. Ése es el motivo por el que debes remplazar el favicon que viene por defecto por el tuyo propio antes del despliegue.

Simplemente sustituye el archivo `web/favicon.ico`.

Para generar favicons, puedes:

* Utilizar herramientas online como [favicon.cc](http://www.favicon.cc) con el fin de generar archivos `.ico`;
* Utilizar un PNG como icono. En ese caso debes definir un `link` en tu HTML: `<link rel="icon" type="image/png" href="tuFavicon.png">`
