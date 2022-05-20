# Samba
Installation du serveur Samba sous Linux (Debian 8)

# Installation

- Etape 1: connectez-vous à votre machine virtuelle en entrant votre login et votre mot de passe d'utilisateur; <br>
- Etape 2: entrez en tant que super utilisateur, tapez la commande `su` et entrez votre mot de passe de super utilisateur; <br>
- Etape 3: tapez la commande suivante : `apt-get install samba` pour installer samba; <br>
- Etape 4: vérifiez si samba a bien été installé avec la commande : `/etc/init.d/samba status` <br>
    Le texte en vert signifie que samba a bien été installé;
- Etape 5: effectuez la commande suivante `nano /etc/samba/samba.conf`