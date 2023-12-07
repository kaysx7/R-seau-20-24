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

vérifiez que le serveur SSH tourne actuellement sur le port 22/tcp

``````````
[kayss@router ~]$ ss -tn
State Recv-Q Send-Q Local Address:Port Peer Address:Port Process
ESTAB 0      0         10.7.1.254:22       10.7.1.1:21739
``````````
vérifiez que le serveur SSH est disponible actuellement sur TOUTES les IPs de la machine

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

Toujours avec la même commande ss vous devriez voir que : le serveur SSH écoute désormais sur 10.7.1.11 uniquement le serveur SSH écoute désormais sur le port choisi

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