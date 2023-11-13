# tp4 

🌞 Déterminer

- L'adresse du serveur DHCP

```
Serveur DHCP . . . . . . . . . . . . . : 192.168.5.254
```
- L'heure exacte à laquelle vous avez obtenu votre bail DHCP


```
 Bail obtenu. . . . . . . . . . . . . . : jeudi 9 novembre 2023 09:30:26
 ```

- L'heure exacte à laquelle il va expirer

```
 vendredi 10 novembre 2023 09:24:12
 ```

🌞 Capturer un échange DHCP

- Forcer votre OS à refaire un échange DHCP complet
- Utiliser Wireshark pour capturer les 4 trames DHCP
  
``````
PS C:\WINDOWS\system32> ipconfig /release

Configuration IP de Windows

Aucune opération ne peut être effectuée sur Ethernet 2 lorsque
son média est déconnecté.
Aucune opération ne peut être effectuée sur Connexion au réseau local* 1 lorsque
son média est déconnecté.

Carte inconnue Connexion au réseau local :

   Statut du média. . . . . . . . . . . . : Média déconnecté
   Suffixe DNS propre à la connexion. . . :

Carte Ethernet Ethernet 2 :

   Statut du média. . . . . . . . . . . . : Média déconnecté
   Suffixe DNS propre à la connexion. . . :

Carte Ethernet Ethernet 3 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::2c62:a90d:4377:c6%10
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.56.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :

Carte Ethernet Ethernet 4 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::1c1:6b45:9b7e:293a%9
   Adresse IPv4. . . . . . . . . . . . . .: 10.3.1.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :

Carte Ethernet Ethernet 5 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::3754:39e6:1cd9:dc52%17
   Adresse IPv4. . . . . . . . . . . . . .: 10.3.2.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :

Carte réseau sans fil Connexion au réseau local* 1 :

   Statut du média. . . . . . . . . . . . : Média déconnecté
   Suffixe DNS propre à la connexion. . . :

Carte réseau sans fil Connexion au réseau local* 2 :

   Statut du média. . . . . . . . . . . . : Média déconnecté
   Suffixe DNS propre à la connexion. . . :

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::bea3:6d81:698c:40d5%4
   Passerelle par défaut. . . . . . . . . :

Carte Ethernet VMware Network Adapter VMnet1 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::5e93:4948:226:601e%22
   Passerelle par défaut. . . . . . . . . :

Carte Ethernet VMware Network Adapter VMnet8 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::b0e0:21c:e45e:6219%24
   Passerelle par défaut. . . . . . . . . :
   ``````

🌞 Analyser la capture Wireshark

``````
La Tram 2 contient les infos pour le client (DHCP)
``````

🦈 tp4_dhcp_client.pcapng

voir github

## II. Serveur DHCP

🌞 Preuve de mise en place

``````

[kayss@dhcp.tp4.b1 ~]$ ping youtube.com
PING youtube.com (142.250.179.110) 56(84) bytes of data.
64 bytes from reflectededge.reflected.net (142.250.179.110): icmp_seq=1 ttl=53 time=15.4 ms
64 bytes from reflectededge.reflected.net (142.250.179.110): icmp_seq=2 ttl=53 time=14.7 ms
64 bytes from reflectededge.reflected.net (142.250.179.110): icmp_seq=3 ttl=53 time=25.1 ms
^C
--- youtube.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2004ms
rtt min/avg/max/mdev = 14.719/18.407/25.135/4.764 ms
``````
``````
[kayss@node1.tp4.b1 ~]$ ping youtube.com
PING youtube.com (142.250.179.110) 56(84) bytes of data.
64 bytes from 142.250.179.110 (142.250.179.110): icmp_seq=1 ttl=55 time=14.5 ms
64 bytes from 142.250.179.110 (142.250.179.110): icmp_seq=2 ttl=55 time=26.5 ms
64 bytes from 142.250.179.110 (142.250.179.110): icmp_seq=3 ttl=55 time=28.2 ms
^C
--- youtube.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 14.465/23.051/28.193/6.110 ms
``````
``````
[kayss@node2.tp4.b1 ~]$ traceroute 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  _gateway (10.4.1.254)  0.591 ms  0.597 ms  0.546 ms
 2  10.0.3.2 (10.0.3.2)  30.577 ms  30.570 ms  30.505 ms
 ```````
 🌞 Serveur DHCP

 installation du logiciel

 ````
 [kayss@dhcp.tp4.b1 ~]$ dnf -y install dhcp-server
 ``````

 🌞 Rendu
``````
 [kayss@dhcp ~]$ sudo nano /etc/dhcp/dhcpd.conf
[kayss@dhcp ~]$ sudo cat /etc/dhcp/dhcpd.conf

option domain-name     "tp4.dhcp";
authoritative;
subnet 10.4.1.0 netmask 255.255.255.0 {
    range dynamic-bootp 10.4.1.137 10.4.1.237;
    option broadcast-address 10.4.1.255;
}
``````
``````
[kayss@dhcp ~]$ sudo systemctl enable --now dhcpd
Created symlink /etc/systemd/system/multi-user.target.wants/dhcpd.service → /usr/lib/systemd/system/dhcpd.service.
[kayss@dhcp ~]$ sudo firewall-cmd --add-service=dhcp
success
[kayss@dhcp ~]$ sudo firewall-cmd --runtime-to-permanent
success
``````
🌞 Test
``````
[kayss@dhcp ~]$ sudo cat /etc/sysconfig/network-scripts/ifcfg-enp0s3
DEVICE=enp0s3

BOOTPROTO=dhcp
ONBOOT=yes
``````
🌞 Prouvez que node1 a bien récupéré une IP dynamiquement

``````
[rocky@localhost ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:de:36:da brd ff:ff:ff:ff:ff:ff
    inet 11.5.1.105/24 brd 11.5.1.255 scope global dynamic noprefixroute enp0s3
       valid_lft 336sec preferred_lft 336sec
    inet6 fe80::a00:27ff:fede:36da/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
``````
``````
[rocky@localhost ~]$ nmcli con show enp0s3
``````
``````
[rocky@localhost ~]$ ping 11.5.1.250
PING 11.5.1.250 (11.5.1.250) 56(84) bytes of data.
64 bytes from 11.5.1.250: icmp_seq=1 ttl=64 time=0.285 ms
64 bytes from 10.5.1.250: icmp_seq=2 ttl=64 time=0.395 ms
^C
--- 11.5.1.250 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1036ms
rtt min/avg/max/mdev = 0.285/0.340/0.395/0.055 ms
[rocky@localhost ~]$ ping 11.5.1.69
PING 11.5.1.69 (11.5.1.69) 56(84) bytes of data.
64 bytes from 11.5.1.69: icmp_seq=1 ttl=64 time=0.407 ms
64 bytes from 11.5.1.69: icmp_seq=2 ttl=64 time=0.349 ms
^C
--- 11.5.1.69 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1044ms
rtt min/avg/max/mdev = 0.349/0.378/0.407/0.029 ms
``````
🌞 Bail DHCP serveur
``````
[rocky@dhcp ~]$ cat /var/lib/dhcpd/dhcpd.leases
# The format of this file is documented in the dhcpd.leases(5) manual page.
# This lease file was written by isc-dhcp-4.4.2b1

# authoring-byte-order entry is generated, DO NOT DELETE
authoring-byte-order little-endian;

lease 10.4.1.137 {
  starts 0 2023/11/09 14:37:07;
  ends 1 2023/11/09 20:37:07;
  tstp 1 2023/11/09 20:37:07;
  cltt 0 2023/11/09 14:37:07;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:de:36:da;
  uid "\001\010\000'\3366\332";
}
server-duid "\000\001\000\001,\332\237\214\010\000'%\270\250";
``````

🌞 Nouvelle conf !

``````
[rocky@dhcp ~]$ sudo cat /etc/dhcp/dhcpd.conf
option domain-name     "tp4.dhcp";
option domain-name-servers     1.1.1.1;
default-lease-time 21600;
max-lease-time 21600;
authoritative;
subnet 11.5.1.105 netmask 255.255.255.0 {
    range dynamic-bootp 11.5.1.137 11.5.1.237;
    option broadcast-address 11.5.1.255;
    option routers 11.5.1.254;
}
``````
``````
[rocky@dhcp ~]$ sudo systemctl restart dhcpd
``````
🌞 Test !
``````
[rocky@localhost ~]$ sudo cat /etc/resolv.conf
``````
``````
[rocky@localhost ~]$ ip r s
default via 11.5.1.254 dev enp0s3 proto dhcp src 11.5.1.138 metric 100
``````
``````
[rocky@dhcp ~]$ cat /var/lib/dhcpd/dhcpd.leases
lease 10.4.1.137 {
  starts 0 2023/11/11 19:41:31;
  ends 1 2023/11/11 01:41:31;  
  tstp 1 2023/11/11 01:41:31;
  cltt 0 2023/11/11 19:41:31;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:de:36:da;
  uid "\001\010\000'\3366\332";
}
server-duid "\000\001\000\001,\332\237\214\010\000'%\270\250";
``````
``````
[rocky@localhost ~]$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=110 time=29.3 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=110 time=37.0 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=110 time=31.2 ms
^C
--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2004ms
rtt min/avg/max/mdev = 29.268/32.503/37.043/3.305 ms
``````
``````
[rocky@localhost ~]$ ping youtube.com
PING youtube.com (172.217.18.206) 56(84) bytes of data.
64 bytes from ham02s14-in-f206.1e100.net (172.217.18.206): icmp_seq=1 ttl=115 time=30.7 ms
64 bytes from par10s38-in-f14.1e100.net (172.217.18.206): icmp_seq=2 ttl=115 time=28.9 ms
64 bytes from par10s38-in-f14.1e100.net (172.217.18.206): icmp_seq=3 ttl=115 time=27.8 ms
^C
--- youtube.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2004ms
rtt min/avg/max/mdev = 27.813/29.147/30.742/1.209 ms
``````