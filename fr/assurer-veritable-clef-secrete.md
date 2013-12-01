Assurer une véritable sécurité avec la clé secrète

Assurez-vous que votre serveur de production utilise une clé secrète personnalisée. Vérifiez dans votre fichier `app/config/parameters.yml` :

    secret:  please_use_a_real_secret_here

Par défaut la clé secrète *n'est pas* vraiment secrète, vous *devez* la remplacer par une autre générée de façon aléatoire.
