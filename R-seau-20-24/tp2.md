

# TP2 : Ethernet, IP, et ARP

## I. Setup IP

🌞 Mettez en place une configuration réseau fonctionnelle entre les deux machines

``````
    10.10.10.10
    10.10.10.9
    255.255.255.252
    10.10.10.8
    10.10.10.252
``````
🌞 Prouvez que la connexion est fonctionnelle entre les deux machines

``````
ping 10.10.10.9

Envoi d’une requête 'Ping'  10.10.10.9 avec 32 octets de données :
Réponse de 10.10.10.9 : octets=32 temps=46 ms TTL=128
Réponse de 10.10.10.9 : octets=32 temps=56 ms TTL=128
Réponse de 10.10.10.9 : octets=32 temps=74 ms TTL=128
Réponse de 10.10.10.9 : octets=32 temps=72 ms TTL=128

Statistiques Ping pour 10.10.10.9:
Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
Minimum = 46ms, Maximum = 74ms, Moyenne = 62ms  
``````
🌞 Wireshark it

``````
    ICMP 1
``````
## II. ARP my bro

🌞 Check the ARP table
``````