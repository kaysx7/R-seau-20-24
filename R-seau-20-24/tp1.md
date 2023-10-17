# tp1

 Affichez les infos des cartes réseau de votre PC
 ```
 C:\Users\kayss> ipconfig

Configuration IP de Windows


Carte Ethernet Ethernet :

   Statut du média. . . . . . . . . . . . : Média déconnecté
   Suffixe DNS propre à la connexion. . . :

Carte Ethernet Ethernet 2 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::2289:3f9a:c875:ffa4%3
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.56.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :

   ```
   Affichez votre gateway
   ```
C:\Users\kayss> ipconfig

   Carte réseau sans fil Wi-Fi :
suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::dbd0:1c59:2ff9:b253%17
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.48.124
   Masque de sous-réseau. . . . . . . . . : 255.255.252.0
   Passerelle par défaut. . . . . . . . . : 10.33.51.254
   ```
   Determiner la MAC de la passerelle
   ```
C:\Users\kayss> arp -a
   10.33.51.254 7c-5a-1c-cb-fd-a4 dynamique
   ```

   -trouver comment afficher les infomartions sur la carte IP (change selon l'os)
   ```
Suffixe DNS propre à la connexion: 
Description: Intel(R) Wi-Fi 6 AX201 160MHz
Adresse physique: ‎70-D8-23-D5-D2-5C
DHCP activé: Oui
Adresse IPv4: 10.33.48.124
Masque de sous-réseau IPv4: 255.255.252.0
Bail obtenu: lundi 16 octobre 2023 09:13:18
Bail expirant: mardi 17 octobre 2023 09:13:08
Passerelle par défaut IPv4: 10.33.51.254
Serveur DHCP IPv4: 10.33.51.254
Serveurs DNS IPv4: 10.33.10.2, 8.8.8.8
Serveur WINS IPv4: 
NetBIOS sur TCP/IP activé: Oui
Adresse IPv6 locale de lien: fe80::dbd0:1c59:2ff9:b253%17
Passerelle par défaut IPv6: 
Serveur DNS IPv6: 
```
2. Modifications des informations
   
A. Modification d'adresse IP (part 1)

```
Adresse Ip : 10.33.1.14
Masque de sous-Réseau : 255.255.252.0
Internet n'est plus présent
j'ai perdu l'acces a Internet par le simple fait que j'ai utilisé la même IP que quelqu'un d'autre
```
II. Exploration locale en duo

3. Modification d'adresse IP
```
C:\Users\kayss>ipconfig

Configuration IP de Windows


Carte Ethernet Ethernet :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::e4c7:fbc7:af73:343b%18
   Adresse IPv4. . . . . . . . . . . . . .: 10.10.10.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :
   ```
 Vérifier que les deux machines se joignent
 ```
 C:\Users\kayss>ping 10.10.10.2

Envoi d’une requête 'Ping'  10.10.10.2 avec 32 octets de données :
Réponse de 10.10.10.2 : octets=32 temps=2 ms TTL=128
Réponse de 10.10.10.2 : octets=32 temps=1 ms TTL=128
Réponse de 10.10.10.2 : octets=32 temps=2 ms TTL=128
Réponse de 10.10.10.2 : octets=32 temps=2 ms TTL=128

Statistiques Ping pour 10.10.10.2:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 1ms, Maximum = 2ms, Moyenne = 1ms
```
    
Déterminer l'adresse MAC de votre correspondant
```
C:\Users\kayss>arp -a
   Interface : 10.10.10.1 --- 0x12
  Adresse Internet      Adresse physique      Type
  10.10.10.2            3c-7c-3f-5f-70-fa     dynamique
  10.10.10.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
```


    

