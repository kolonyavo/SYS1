# NFS
Installation du serveur NFS sous Linux (Debian 8)

# Utilisation
NFS peut être utilisé pour partager des répertoires de fichiers entre plusieurs utilisateurs sur un même réseau.

# Installation
    a) Installer du côté serveur: `apt-get install nfs-kernel-server nfs-common`
    b) Installer du côté client: `apt-get install nfs-commun`

### Exporter des répertoires sur le serveur
1) Créez le répertoire /home/client1
    - Du coté serveur:

    mkdir /home/client1 
    chown personne:nogroup /home/client1 
    chmod 755 /home/client1

2) Modifier /etc/exports où vous "exportez" vos partages NFS. Spécifiez /home/client1 et /var/www comme partages NFS et dites à NFS d'accéder à /home/client1 en tant qu'utilisateur personne 

`homme 5 exporte`

    vi /etc/exports
    /home/client1 192.168.0.101(rw,sync,no_subtree_check)
    /var/www 192.168.0.101(rw,sync,fsid=0,crossmnt,no_subtree_check,no_root_squash)
(L' option no_root_squash fait que /var/www sera accessible en tant que root.)

3) Pour appliquer les modifications dans /etc/exports , redémarez le serveur nfs du noyau `/etc/init.d/nfs-kernel-server restart`

### Monter les partages NFS sur le Client
    - Du coté client:

1) Créez les répertoires où vous voulez monter les partages NFS, par exemple :

    mkdir -p /mnt/nfs/home/client1 
    mkdir -p /var/www

* Si le répertoire /var/www existe déjà sur votre serveur, arrêtez apache, renommez le répertoire et créez un nouveau répertoire vide comme point de montage

    /etc/init.d/apache2 stop 
    mv /var/www /var/www_bak 
    mkdir -p /var/www

2) Montez les comme suit :

    monter 192.168.0.100:/home/client1 /mnt/nfs/home/client1 
    monter 192.168.0.100:/var/www /var/www

3) Vous devriez maintenant voir les deux partages NFS dans les sorties de

`df-h` et `monter`

4) Sur le client, vous pouvez maintenant essayer de créer des fichiers de test sur les partages NFS :

client:

    touchez /mnt/nfs/home/client1/test.txt 
    touchez /var/www/test.txt

Allez maintenant sur le serveur et vérifiez si vous pouvez voir les deux fichiers de test :

serveur:

    ls -l /home/client1/
    [ root@server  ~]# ls -l /home/client1 
    total 0 
    -rw-r--r-- 1 personne nogroup 0 Feb 02 16:58 test.txt 
    [ root@server  ~]#
    ls -l /var/nfs
    [ root@server  ~]# ls -l /var/www 
    total 0 
    -rw-r--r-- 1 root root 0 Feb 02 16:58 test.txt 
    [ root@server  ~]#

(Veuillez noter les différentes propriétés des fichiers de test : le partage NFS /home/client1 est accessible en tant que personne / nogroup etn'appartient à personne / nogroup ; le partage /var/www est accessible en tant que root , donc /var/www/test.txt appartient à l'utilisateur et au groupe root .)