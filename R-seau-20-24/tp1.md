# tp1
# I-Exploration locale en solo

## 1 affichage d'information sur la pile TCP/IP locale
🌞 Affichez les infos des cartes réseau de votre PC
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
   🌞 Affichez votre gateway
   ```
C:\Users\kayss> ipconfig

   Carte réseau sans fil Wi-Fi :
suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::dbd0:1c59:2ff9:b253%17
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.48.124
   Masque de sous-réseau. . . . . . . . . : 255.255.252.0
   Passerelle par défaut. . . . . . . . . : 10.33.51.254
   ```
🌞 Déterminer la MAC de la passerelle
   ```
C:\Users\kayss> arp -a
   10.33.51.254 7c-5a-1c-cb-fd-a4 dynamique
   ```

🌞 Trouvez comment afficher les informations sur une carte IP (change selon l'OS
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
## 2. Modifications des informations
   
A. Modification d'adresse IP (part 1)

🌞 Utilisez l'interface graphique de votre OS pour changer d'adresse IP :

```
Adresse Ip : 10.33.1.14
Masque de sous-Réseau : 255.255.252.0
Internet n'est plus présent
```
🌞 Il est possible que vous perdiez l'accès internet. Que ce soit le cas ou non, expliquez pourquoi c'est possible de perdre son accès internet en faisant cette opération

j'ai perdu l'acces a Internet par le simple fait que j'ai utilisé la même IP que quelqu'un d'autre

# II. Exploration locale en duo


## 3. Modification d'adresse IP
   
   🌞 Modifiez l'IP des deux machines pour qu'elles soient dans le même réseau

 ```
 panneau de configuration > réseau et internet > centre réseau et partage > Wifi > Propriété > Protocole internet version 4: fAdresse ip : 10.10.10.2 masque de sous réseau : 255.255.255.0
```
🌞 Vérifier à l'aide d'une commande que votre IP a bien été 
changée

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



🌞 Vérifier que les deux machines se joignent




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
    
🌞 Déterminer l'adresse MAC de votre correspondant
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
### 4/ PETIT CHAT PRIVÉ

🌞 sur le PC client

```
./nc.exe 10.10.10.09 8888
bonjour
salut
wesh
```
🌞 Visualiser la connexion en cours
```
netstat -a -n -b | Select-String "8888" -Context 0,1

>   TCP    10.10.10.15:51674      10.10.10.9:8888           ESTABLISHED
[nc.exe]
```
🌞Pour aller un peu plus loin
```
.\nc.exe -l -p 8888 -s 10.10.10.15
blabla
dvdvvd
```
### 5. FIREWALL

🌞 Activez et configurez votre firewall
```
ping 10.10.10.9

Envoi d’une requête 'Ping'  10.10.10.9 avec 32 octets de données :
Réponse de 10.10.10.9 : octets=32 temps=3 ms TTL=128
Réponse de 10.10.10.9 : octets=32 temps=3 ms TTL=128
Réponse de 10.10.10.9 : octets=32 temps=2 ms TTL=128
Réponse de 10.10.10.9 : octets=32 temps=3 ms TTL=128
Statistiques Ping pour 10.10.10.9:
Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
Minimum = 2ms, Maximum = 3ms, Moyenne = 2ms
```
### 6. Utilisation d'un des deux comme gateway

🌞Tester l'accès internet
```
ping 1.1.1.1

Envoi d’une requête 'Ping'  1.1.1.1 avec 32 octets de données :
Réponse de 1.1.1.1 : octets=32 temps=11 ms TTL=57
Réponse de 1.1.1.1 : octets=32 temps=12 ms TTL=57
Réponse de 1.1.1.1 : octets=32 temps=11 ms TTL=57
Réponse de 1.1.1.1 : octets=32 temps=13 ms TTL=57

Statistiques Ping pour 1.1.1.1:
Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
Minimum = 11ms, Maximum = 13ms, Moyenne = 11ms
```
🌞 Prouver que la connexion Internet passe bien par l'autre PC

```
tracert 10.10.10.9

Détermination de l’itinéraire vers 10.10.10.9 avec un maximum de 30 sauts.

1     4 ms     3 ms     5 ms  10.33.51.254
2     3 ms     3 ms     2 ms  237.252.159.77.rev.sfr.net [77.159.252.237]
3     6 ms     4 ms     5 ms  108.97.30.212.rev.sfr.net [212.30.97.108] 4     4 ms     4 ms     4 ms  205.212.192.77.rev.sfr.net [77.192.212.205]
5    24 ms    24 ms    23 ms  2.144.6.194.rev.sfr.net [194.6.144.2]
6    21 ms    20 ms    21 ms  122.220.96.84.rev.sfr.net [84.96.220.122]
7    22 ms    22 ms    21 ms  154.224.63.86.rev.sfr.net [86.63.224.154]
8    26 ms    34 ms    25 ms  185.225.63.86.rev.sfr.net [86.63.225.185]
9    27 ms    25 ms    28 ms  174.225.63.86.rev.sfr.net [86.63.225.174]
10    27 ms    26 ms    26 ms  169.225.63.86.rev.sfr.net [86.63.225.169]
```
# III. Manipulations d'autres outils/protocoles côté client