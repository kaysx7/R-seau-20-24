# tp 7

# II. SSH

## 1. Fingerprint

🌞 Effectuez une connexion SSH en vérifiant le fingerprint

- en rendu je veux voir le message du serveur à la première connexion

- une commande ssh pour se connecter vers john

``````
PS C:\Users\kayss> ssh kayss@10.7.1.11
The authenticity of host '10.7.1.11 (10.7.1.11)' can't be established.
ED25519 key fingerprint is SHA256:AEtJxrKXGz1+aH+EHgalAhCRFUFx/83LYCM306PkW0I.
This host key is known by the following other names/addresses:
    C:\Users\kayss/.ssh/known_hosts:4: 10.3.1.11
    C:\Users\kayss/.ssh/known_hosts:7: 10.3.1.12
    C:\Users\kayss/.ssh/known_hosts:8: 10.3.1.254
    C:\Users\kayss/.ssh/known_hosts:9: 10.3.2.254
    C:\Users\kayss/.ssh/known_hosts:10: 10.5.1.11
    C:\Users\kayss/.ssh/known_hosts:11: 10.5.1.253
    C:\Users\kayss/.ssh/known_hosts:15: 10.5.1.254
    C:\Users\kayss/.ssh/known_hosts:16: 10.5.1.12
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.7.1.11' to the list of known hosts.
``````
- et je veux aussi une commande qui me montre l'empreinte du serveur
``````
[kayss@john ~]$ sudo ssh-keygen -l -f /etc/ssh/
``````
## 2. Conf serveur SSH

🌞 Consulter l'état actuel

- vérifiez que le serveur SSH tourne actuellement sur le port 22/tcp

``````````
[kayss@router ~]$ ss -tn
State Recv-Q Send-Q Local Address:Port Peer Address:Port Process
ESTAB 0      0         10.7.1.254:22       10.7.1.1:21739
``````````
- vérifiez que le serveur SSH est disponible actuellement sur TOUTES les IPs de la machine

````````
[kayss@router ~]$ ss -lt
State  Recv-Q Send-Q Local Address:Port Peer Address:PortProcess
LISTEN 0      128          0.0.0.0:ssh       0.0.0.0:*
LISTEN 0      128             [::]:ssh          [::]:*
````````
🌞 Modifier la configuration du serveur SSH

``````````
[kayss@router ~]$ sudo nano /etc/ssh/sshd_config
Port 22500
#AddressFamily any
ListenAddress 10.7.1.254
#ListenAddress ::
``````````
🌞 Prouvez que le changement a pris effet

- Toujours avec la même commande ss vous devriez voir que : le serveur SSH écoute désormais sur 10.7.1.11 uniquement le serveur SSH écoute désormais sur le port choisi

````````
[kayss@router ~]$ sudo ss -lntp
State      Recv-Q     Send-Q          Local Address:Port            Peer Address:Port     Process
LISTEN     0          128                10.7.1.254:22500                0.0.0.0:*         users:(("sshd",pid=1036,fd=3))
````````
🌞 Effectuer une connexion SSH sur le nouveau port

````````
PS C:\Users\kayss> ssh kayss@router -p 22500
The authenticity of host '[router]:22500 ([10.7.1.254]:22500)' can't be established.
ED25519 key fingerprint is SHA256:LiWk49XIVPOBhCg7+FRoMGuM+WQZInba139U+eUhqtM.
This host key is known by the following other names/addresses:
    C:\Users\kayss/.ssh/known_hosts:5: 10.3.1.11
    C:\Users\kayss/.ssh/known_hosts:8: 10.3.1.12
    C:\Users\kayss/.ssh/known_hosts:9: 10.3.2.12
    C:\Users\kayss/.ssh/known_hosts:10: 10.3.2.254
    C:\Users\kayss/.ssh/known_hosts:11: 10.3.1.254
    C:\Users\kayss/.ssh/known_hosts:12: 10.4.1.253
    C:\Users\kayss/.ssh/known_hosts:13: 10.4.1.254
    C:\Users\kayss/.ssh/known_hosts:14: 10.4.1.12
    (12 additional names omitted)
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[router]:22500' (ED25519) to the list of known hosts.
````````
## 3-Connexion par clé

### B. Manips Let's go : 

🌞 Générer une paire de clés

``````
PS C:\Users\kayss> ls .\.ssh\id_rsa.pub
 Répertoire : C:\Users\kayss\.ssh
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        07/12/2023     16:22            736 id_rsa.pub
````````

🌞 Déposer la clé publique sur une VM

````````
$ ssh-copy-id kayss@10.7.1.11
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/c/Users/kayss/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed

/usr/bin/ssh-copy-id: WARNING: All keys were skipped because they already exist on the remote system.
(if you think this is a mistake, you want to use -f option)
````````
🌞 Connectez-vous en SSH à la machine

````````````
PS C:\Users\kayss> ssh kayss@10.7.1.11
Last login: Fri Dec 07 16:42:34 2023 from 10.7.1.1
``````````````
🌞 Supprimer les clés sur la machine router.tp7.b1

````````
[kayss@router ssh]$ sudo rm ssh_host_*
[sudo] password for kayss:
````````
🌞 Regénérez les clés sur la machine router.tp7.b1

````````
[kayss@router ~]$ sudo sudo ssh-keygen -A

[kayss@router ~]$ sudo systemctl restart sshd
````````
🌞 Tentez une nouvelle connexion au serveur

- le message nous indique que la clé enregistré pour le router n'est pas la même que celle de la nouvelle clé du router

````````
$ ssh kayss@10.7.1.254
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ED25519 key sent by the remote host is
SHA256:G6kyYtRQS9xbhJr5i/2pOJn4uf5ZPXee7nuznWBJRFi1UVPk.
Please contact your system administrator.
Add correct host key in /c/Users/kayss/.ssh/known_hosts to get rid of this message.
Offending ED25519 key in /c/Users/kayss/.ssh/known_hosts:17
Host key for 10.7.1.254 has changed and you have requested strict checking.
Host key verification failed.
````````
````````
PS C:\Users\kayss> ssh kayss@router -p 22500
The authenticity of host '[router]:22500 ([10.7.1.254]:22500)' can't be established.
ED25519 key fingerprint is SHA256:G6kyYtRQS9xbhJr5i/2pOJn4uf5ZPXee7nuznWBJRFi1UVPk.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[router]:22500' (ED25519) to the list of known hosts.
kayss@router's password:
Last login: Fri Dec 07 16:42:34 2023 from 10.7.1.1
````````
# III. Web sécurisé

🌞 Montrer sur quel port est disponible le serveur web

``````
[kayss@web ~]$ ss -tnl
State  Recv-Q Send-Q Local Address:Port Peer Address:PortProcess
LISTEN 0      511          0.0.0.0:70        0.0.0.0:*
``````
🌞 Générer une clé et un certificat sur web.tp7.b1

````````


[kayss@web ~]$ openssl req -new -newkey rsa:2048 -days 365 -nodes -x509 -keyout server.key -out server.crt
....+.....+.......+..+...+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*......+.......+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.......+..+....+...............+......+...........+....+......+...........................+.....+...+...+......+.+............+........+....+........+......+.......+.....+....+.....+....+.....+................+...+...+........+......+....+..+.........+.............+..+....+.....+.+...+........+....+.....+.+........+...................+..+.+...............+............+..+.............+.....+.+......+........+...+...+..........+...........+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
...+.......+..+.+......+...+..+.+.........+...........+....+.....+.+........+....+......+..+.......+..+...+.+.........+............+........+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.....+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.+.....+.......+.....+.........+.+...+..+.......+......+......+.........+..+...+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:dd
State or Province Name (full name) []:kayss
Locality Name (eg, city) [Default City]:bordeaux
Organization Name (eg, company) [Default Company Ltd]:idk
Organizational Unit Name (eg, section) []:kayss
Common Name (eg, your name or your server's hostname) []:kayss
Email Address []:kayss
[kayss@web ~]$ sudo mv server.key /etc/pki/tls/private/web.tp7.b1.key
[sudo] password for kayss:
[kayss@web ~]$ sudo mv server.crt /etc/pki/tls/certs/web.tp7.b1.crt
[kayss@web ~]$ sudo chown nginx:nginx /etc/pki/tls/private/web.tp7.b1.key
[kayss@web ~]$ sudo chown nginx:nginx /etc/pki/tls/certs/web.tp7.b1.crt
[kayss@web ~]$ sudo chmod 0400 /etc/pki/tls/private/web.tp7.b1.key
[kayss@web ~]$ sudo chmod 0444 /etc/pki/tls/certs/web.tp7.b1.crt
````````
🌞 Conf firewall
````````
[kayss@web ~]$ sudo firewall-cmd --add-port=443/tcp --permanent
success
[kayss@web ~]$ sudo firewall-cmd --reload
success
````````

🌞 Redémarrez NGINX

````````````
[kayss@web ~]$ sudo systemctl restart nginx
``````````````

🌞 Prouvez que NGINX écoute sur le port 443/tcp

````````
[kayss@web ~]$ sudo ss -tnl | grep 443
LISTEN 0      511        10.7.1.12:443       0.0.0.0:*
`````````
🌞 Visitez le site web en https

````````
[kayss@web ~]$ curl -k https://10.7.1.12
<h1>MEOW</h1>
````````