Use Custom Favicon
basis
You don't want the Symfony logo to appear in your visitors' browser. That's why you must replace the default favicon with your own before deployment.

Just replace the file `web/favicon.ico`.

To make favicons, you can:
* Use online tools like [favicon.cc](http://www.favicon.cc) in order to generate `.ico` files;
* Use a PNG icon. In that case you must define a `link` in your HTML: `<link rel="icon" type="image/png" href="yourFavIcon.png">`
