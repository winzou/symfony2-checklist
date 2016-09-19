Check the command line execution context
basic
Symfony2 commands are executed in the ```dev``` environment, generating both cache and log unwanted files.

Set the environment variable ```SYMFONY_ENV``` to ```prod``` in order to ensure that all the command are executed on the Production context, or verify that all the command are executed with the option ```--env=prod```.