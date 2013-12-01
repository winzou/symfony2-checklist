Assurer une véritable sécurité avec la clé secrète

Assurez-vous que votre serveur de production utilise une clé secrète personnalisé. Vérifiez dans votre fichier `app/config/parameters.yml` : 

    secret:  please_use_a_real_secret_here

Par défault la clé secrète *n'est pas* vraiment secrète, vous *devez* la remplacer par une autre généré de façon aléatoire.
