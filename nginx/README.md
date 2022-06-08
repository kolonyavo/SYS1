# Nginx
Installation du serveur Nginx sous Linux (Debian 8)

# Utilisation
Nginx permet de servir des fichiers statiques et comme un proxy pour les requêtes dynamiques typiquement acheminées en utilisant une interface FastCGI vers un ou des serveurs applicatifs avec un mécanisme de répartition de charge.

# Installation

- Etape 1: connectez-vous à votre machine virtuelle en entrant votre login et votre mot de passe d'utilisateur; <br>
- Etape 2: entrez en tant que super utilisateur, tapez la commande `su` et entrez votre mot de passe de super utilisateur; <br>
- Etape 3: tapez la commande suivante : `apt-get install nginx` pour installer nginx; <br>
- Etape 4: vérifiez si nginx a bien été installé avec la commande : `/etc/init.d/nginx status` <br> <br>
    <img src="status.png" alt="image" width="70%" height="70%"> <br>
    le texte en vert signifie que nginx a bien été installé;

# Configuration
* Effectuez la commande suivante `nano /etc/nginx/nginx.conf`.
* Créez un dossier dans le www du nginx `mkdir /var/www/nom du domaine du site` ce dossier va nous permettre de stocker les fichier de notre site qui est notre racine
* Déterminez du proprieter du dossier du l'utilisateur de nginx `chown -R www-data:www-data /var/www/nom du site/`
* Apppliquez les droits `chmod 755 /var/www/nom du site/`
* Créez une page index.html pour la racine `nano /var/www/nom du site/index.html`
* Créez du fichier de configuration (nano /etc/nginx/sites-available/appellation du site):
exemple: server{
        listen 80;
        listen [::]:80;

        root/var/www/nom du site;

        index index.html;
        server_name nom du site www nom du site;

        location / {
            try_files $uri $uri/ =404;
        }
    }
* Mettez la configuration permanente `ln -s /etc/nginx/site-available/nom du site /etc/nginx/sites-enabled/nom du site`
* Verifiez la configuration de notre nginx avec la commande `nginx -t`
* Il est l'heure de redémarer le serveur avec la commande : `/etc/init.d/nginx restart`