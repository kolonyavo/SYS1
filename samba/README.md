# Samba
Installation du serveur Samba sous Linux (Debian 8)

# Utilisation
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