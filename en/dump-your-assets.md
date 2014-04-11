In the prod environment, your JS and CSS files are represented by a single tag each. In other words, instead of seeing each JavaScript file you're including in your source, you'll likely just see something like this:

    <script src="/js/abcd123.js"></script>
    
Moreover, that file does not actually exist, nor is it dynamically rendered by Symfony (as the asset files are in the dev environment). This is on purpose - letting Symfony generate these files dynamically in a production environment is just too slow.

Instead, each time you use your app in the prod environment (and therefore, each time you deploy), you should run the following task:

	$ php app/console assetic:dump --env=prod --no-debug
	
This will physically generate and write each file that you need (e.g. /js/abcd123.js). If you update any of your assets, you'll need to run this again to regenerate the file.

* _See [Asset Management documentation](http://symfony.com/doc/current/cookbook/assetic/asset_management.html#dumping-asset-files-in-the-prod-environment)_
