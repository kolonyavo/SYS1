# VSFTPD
Installation du serveur VSFTPD sous Linux (Debian 8)

# Utilisation
VSFTPD est utilisé sur Internet pour l'échange de fichiers, il conçu avec la problématique d'une sécurité maximale.

## Installation
- Etape 1: connectez-vous à votre machine virtuelle en entrant votre login et votre mot de passe d'utilisateur; <br>
- Etape 2: entrez en tant que super utilisateur, tapez la commande `su` et entrez votre mot de passe de super utilisateur; <br>
- Etape 3: tapez la commande suivante : `apt-get update` `apt-get install vsftpd` pour installer vsftpd; <br>

## Configuration
Entrez dans le fichier "vsftpd.conf" avec  `nano etc/vsftpd/vsftpd.conf` et définissez ou décommentez ce qui suit :

    annonymous_enable=NO
    local_enabled=YES
    write_enable=YES
    chroot_local_users=YES