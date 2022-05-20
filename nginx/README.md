# Nginx
Installation du serveur Nginx sous Linux (Debian 8)

# Installation

- Etape 1: connectez-vous à votre machine virtuelle en entrant votre login et votre mot de passe d'utilisateur; <br>
- Etape 2: entrez en tant que super utilisateur, tapez la commande `su` et entrez votre mot de passe de super utilisateur; <br>
- Etape 3: tapez la commande suivante : `apt-get install nginx` pour installer nginx; <br>
- Etape 4: vérifiez si nginx a bien été installé avec la commande : `/etc/init.d/nginx status` <br> <br>
    <img src="status.png" alt="image" width="70%" height="70%"> <br> <br>
    le texte en vert signifie que nginx a bien été installé;
- Etape 5: effectuez la commande suivante `nano /etc/nginx/nginx.conf`