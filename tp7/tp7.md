# tp 7

# II. SSH

## 1. Fingerprint

🌞 Effectuez une connexion SSH en vérifiant le fingerprint

- en rendu je veux voir le message du serveur à la première connexion

- une commande ssh pour se connecter vers john

``````
PS C:\Users\debian> ssh kayss@10.7.1.11
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