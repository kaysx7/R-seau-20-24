# tp 6

## TP6 : Un LAN maîtrisé meo ?

Serveur DNS 🌞 Dans le rendu, je veux un cat des 3 fichiers de conf (fichier principal + deux fichiers de zone)

```
[kayss@dns ~]$ sudo cat /var/named/tp6.b1.rev
$TTL 86400
@ IN SOA dns.tp6.b1. admin.tp6.b1. (
    2019061800 ;Serial
    3600 ;Refresh
    1800 ;Retry
    604800 ;Expire
    86400 ;Minimum TTL
)

; Infos sur le serveur DNS lui même (NS = NameServer)
@ IN NS dns.tp6.b1.

; Reverse lookup
101 IN PTR dns.tp6.b1.
11 IN PTR john.tp6.b1.
`````````

``````````
[kayss@dns ~]$ sudo cat /var/named/tp6.b1.db
$TTL 86400
@ IN SOA dns.tp6.b1. admin.tp6.b1. (
    2019061800 ;Serial
    3600 ;Refresh
    1800 ;Retry
    604800 ;Expire
    86400 ;Minimum TTL
)

; Infos sur le serveur DNS lui même (NS = NameServer)
@ IN NS dns.tp6.b1.

; Enregistrements DNS pour faire correspondre des noms à des IPs
dns       IN A 10.6.1.101
john      IN A 10.6.1.11

````````````

````````
[kayss@dns ~]$ sudo cat /etc/named.conf
[sudo] password for kayss:

options {
        listen-on port 51 { 127.0.0.1; any; };
        listen-on-v6 port 51 { ::1; };
        directory       "/var/named";
        dump-file       "/var/named/data/cache_dump.db";
        statistics-file "/var/named/data/named_stats.txt";
        memstatistics-file "/var/named/data/named_mem_stats.txt";
        secroots-file   "/var/named/data/named.secroots";
        recursing-file  "/var/named/data/named.recursing";
        allow-query     { localhost; any; };
        allow-query-cache { localhost; any; };

        recursion yes;

        dnssec-validation yes;

        managed-keys-directory "/var/named/dynamic";
        geoip-directory "/usr/share/GeoIP";

        pid-file "/run/named/named.pid";
        session-keyfile "/run/named/session.key";

        /* https://fedoraproject.org/wiki/Changes/CryptoPolicy */
        include "/etc/crypto-policies/back-ends/bind.config";
};

logging {
        channel default_debug {
                file "data/named.run";
                severity dynamic;
        };
};

zone "." IN {
        type hint;
        file "named.ca";
};

include "/etc/named.rfc1912.zones";
include "/etc/named.root.key";

# référence vers notre fichier de zone
zone "tp6.b1" IN {
     type master;
     file "tp6.b1.db";
     allow-update { none; };
     allow-query {any; };
};
# référence vers notre fichier de zone inverse
zone "1.4.10.in-addr.arpa" IN {
     type master;
     file "tp6.b1.rev";
     allow-update { none; };
     allow-query { any; };
};
````````
un systemctl status named qui prouve que le service tourne bien.

``````````
[kayss@dns ~]$ systemctl status named
● named.service - Berkeley Internet Name Domain (DNS)
     Loaded: loaded (/usr/lib/systemd/system/named.service; enabled; preset: disabled)
     Active: active (running) since Fri 2023-11-17 11:09:40 CET; 12min ago
   Main PID: 4297 (named)
      Tasks: 5 (limit: 4605)
     Memory: 20.4M
        CPU: 39ms
     CGroup: /system.slice/named.service
             └─4297 /usr/sbin/named -u named -c /etc/named.conf
``````````
une commande ss qui prouve que le service écoute bien sur un port
````````
[kayss@dns ~]$ sudo ss -tulpn
Netid State  Recv-Q Send-Q   Local Address:Port   Peer Address:Port Process
udp   UNCONN 0      0            127.0.0.1:323         0.0.0.0:*     users:(("chronyd",pid=676,fd=5))
udp   UNCONN 0      0           10.6.1.101:53          0.0.0.0:*     users:(("named",pid=4297,fd=19))
udp   UNCONN 0      0            127.0.0.1:53          0.0.0.0:*     users:(("named",pid=4297,fd=16))
udp   UNCONN 0      0                [::1]:323            [::]:*     users:(("chronyd",pid=676,fd=6))
udp   UNCONN 0      0                [::1]:53             [::]:*     users:(("named",pid=4297,fd=22))
tcp   LISTEN 0      10          10.6.1.101:53          0.0.0.0:*     users:(("named",pid=4297,fd=21))
tcp   LISTEN 0      10           127.0.0.1:53          0.0.0.0:*     users:(("named",pid=4297,fd=17))
tcp   LISTEN 0      128            0.0.0.0:22          0.0.0.0:*     users:(("sshd",pid=691,fd=3))
tcp   LISTEN 0      4096         127.0.0.1:953         0.0.0.0:*     users:(("named",pid=4297,fd=24))
tcp   LISTEN 0      4096             [::1]:953            [::]:*     users:(("named",pid=4297,fd=25))
tcp   LISTEN 0      128               [::]:22             [::]:*     users:(("sshd",pid=691,fd=4))
tcp   LISTEN 0      10               [::1]:53             [::]:*     users:(("named",pid=4297,fd=23))
````````
🌞 Ouvrez le bon port dans le firewall
``````
[kayss@dns ~]$ sudo ss -tulpn | grep :53
udp   UNCONN 0      0         10.6.1.101:53        0.0.0.0:*    users:(("named",pid=4297,fd=19))
udp   UNCONN 0      0          127.0.0.1:53        0.0.0.0:*    users:(("named",pid=4297,fd=16))
udp   UNCONN 0      0              [::1]:53           [::]:*    users:(("named",pid=4297,fd=22))
tcp   LISTEN 0      10        10.6.1.101:53        0.0.0.0:*    users:(("named",pid=4297,fd=21))
tcp   LISTEN 0      10         127.0.0.1:53        0.0.0.0:*    users:(("named",pid=4297,fd=17))
tcp   LISTEN 0      10             [::1]:53           [::]:*    users:(("named",pid=4297,fd=23))
``````````
ouvrez ce port dans le firewall de la machine dns.tp6.b1 (voir le mémo réseau Rocky)

````````
[kayss@dns ~]$ sudo firewall-cmd --add-port=53/udp --permanent
success
[kayss@dns ~]$ sudo firewall-cmd --reload
success
````````

## 3 Test 


🌞 Sur la machine john.tp6.b1

configurez la machine pour qu'elle utilise votre serveur DNS quand elle a besoin de résoudre des noms

````````
[kayss@john ~]$ ping john.tp6.b1
PING john.tp6.b1(john.tp6.b1 (fe80::a00:27ff:fe68:4adc%enp0s3)) 56 data bytes
64 bytes from john.tp6.b1 (fe80::a00:27ff:fe68:4adc%enp0s3): icmp_seq=1 ttl=64 time=0.024 ms
64 bytes from john.tp6.b1 (fe80::a00:27ff:fe68:4adc%enp0s3): icmp_seq=2 ttl=64 time=0.036 ms
^C64 bytes from fe80::a00:27ff:fe68:4adc%enp0s3: icmp_seq=3 ttl=64 time=0.037 ms

--- john.tp6.b1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2054ms
rtt min/avg/max/mdev = 0.024/0.032/0.037/0.005 ms
````````