Vérifier le contexte d'exécution des commande
basic
Par défaut, l'exécution des commandes via la console se fait en environnement ```dev```, générant à la fois du cache et des logs indésirables.

Pour faire en sorte que l'ensemble des commandes s'exécute en contexte de Production, paramétrez la variable d'environnement ```SYMFONY_ENV``` à la valeur ```prod```.
Sinon, pensez à faire l'inventaire des commandes appelées pour vérifier qu'elles sont toutes exécutées en précisant l'environnement avec l'option ```--env=prod```.