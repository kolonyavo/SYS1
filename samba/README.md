# Samba
Installation du serveur Samba sous Linux (Debian 8)

# Définition
Samba permet d'organiser les autorisations de partage de données et autres services en réseau mais aussi de prendre en charge le rôle d'Active Directory Domain Controllers.

# Installation & Configuration
- Etape 1: connectez-vous à votre machine virtuelle en entrant votre login et votre mot de passe d'utilisateur; <br>
- Etape 2: entrez en tant que super utilisateur, tapez la commande `su` et entrez votre mot de passe de super utilisateur; <br>
- Etape 3: tapez la commande suivante : `apt-get install samba` pour installer samba; <br>
- Etape 4: vérifiez si samba a bien été installé avec la commande : `/etc/init.d/samba status` <br>
    Le texte en vert signifie que samba a bien été installé;
- Etape 5: effectuez la commande suivante `nano /etc/samba/samba.conf`
    Avec le contenu suivant :

    [global] groupe de 
    travail = chaîne de serveur WORKGROUP = 
    serveur Samba %v 
    nom netbios = 
    sécurité debian = 
    mappage utilisateur vers invité = mauvais utilisateur 
    proxy DNS = non

    Remplacez WORKGROUP par le nom du groupe de travail utilisé. Si vous ne connaissez pas le nom du groupe de travail, exécutez cette commande sur le client Windows pour obtenir le nom du groupe de travail :
   `poste de travail de configuration net`

    Enregistrez

- Etape 6: Redémarer le serveur avec la commande : `/etc/init.d/samba restart`

# Utilisation

* Créez le répertoire pour partager les fichiers et changez le groupe en groupe d' utilisateurs :

    mkdir -p /home/shares/allusers 
    chown -R root:users /home/shares/allusers/ 
    chmod -R ug+rwx,o+rx-w /home/shares/allusers/
    mkdir -p /home/shares/anonymous 
    chown -R root:users /home/shares/anonymous/ 
    chmod -R ug+rwx,o+rx-w /home/shares/anonymous/

A la fin du fichier /etc/samba/samba.conf ajoutez les lignes suivantes :
"nano /etc/samba/smb.conf"

* Part du groupe
Il s'agit d'un partage accessible et inscriptible pour tous les membres de notre groupe "utilisateurs". Ajoutez la configuration suivante à la fin du fichier smb.conf.

    [tous les utilisateurs]
    commentaire = Tous les utilisateurs
    chemin = /home/shares/allusers
    utilisateurs valides = @users
    groupe de force = utilisateurs
    créer un masque = 0660
    masque de répertoire = 0771
    inscriptible = oui

* Répertoires personnels
Si vous souhaitez que tous les utilisateurs puissent lire et écrire dans leurs répertoires personnels via Samba, ajoutez les lignes suivantes à /etc/samba/smb.conf (assurez-vous de commenter ou de supprimer la section [homes] existante ) :

    [maisons]
    commentaire = Répertoires personnels
    navigable = non
    utilisateurs valides = %S
    inscriptible = oui
    créer un masque = 0700
    masque de répertoire = 0700

* Pour faire un partage anonyme
Vous aimez avoir un partage sur lequel tous les utilisateurs de votre réseau peuvent écrire ? Attention, ce partage est ouvert à tous sur le réseau, utilisez-le donc uniquement dans les réseaux locaux. Ajoutez un partage anonyme comme celui-ci :

    [anonyme]
    chemin = /home/partages/anonyme
    forcer le groupe = les utilisateurs 
    créent un masque = 0660 
    masque de répertoire = 0771 
    navigable = oui
    inscriptible = oui
    invité ok = oui

Maintenant, nous redémarrons Samba :

* Redémarer le serveur avec la commande : `/etc/init.d/samba restart`