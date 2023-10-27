

# TP3 : On va router des trucs

## I. ARP

### 1. Echange ARP

🌞Générer des requêtes ARP

``````
[kayss@localhost ~]$ ping 10.3.1.12
PING 10.3.1.12 (10.3.1.12) 56(84) bytes of data.
64 bytes from 10.3.1.12: icmp_seq=1 ttl=64 time=0.845 ms
64 bytes from 10.3.1.12: icmp_seq=2 ttl=64 time=0.832 ms
64 bytes from 10.3.1.12: icmp_seq=3 ttl=64 time=1.09 ms
64 bytes from 10.3.1.12: icmp_seq=4 ttl=64 time=0.985 ms
64 bytes from 10.3.1.12: icmp_seq=5 ttl=64 time=1.00 ms
``````


``````
[kayss@localhost ~]$ ip neigh show
10.3.1.12 dev enp0s3 lladdr 08:00:27:c8:89:4b STALE
10.3.1.1 dev enp0s3 lladdr 0a:00:27:00:00:4a DELAY
``````
## 2. Analyse de trames

🌞Analyse de trames

``````
[dany@localhost ~]$ sudo tcpdump
dropped privs to tcpdump
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on enp0s3, link-type EN10MB (Ethernet), snapshot length 262144 bytes
11:19:38.970801 IP localhost.localdomain.ssh > 10.3.1.1.58020: Flags [P.], seq 2227238898:2227238958, ack 1069414303, win 501, length 60
11:19:38.970899 IP localhost.localdomain.ssh > 10.3.1.1.58020: Flags [P.], seq 60:204, ack 1, win 501, length 144
11:19:38.971078 IP localhost.localdomain.ssh > 10.3.1.1.58020: Flags [P.], seq 204:472, ack 1, win 501, length 268
11:19:38.971235 IP 10.3.1.1.58020 > localhost.localdomain.ssh: Flags [.], ack 60, win 8193, length 0

``````

# II. Routage