# tp5

## I. First steps

🌞 Déterminez, pour ces 5 applications, si c'est du TCP ou de l'UDP

``````
netflix.com 
PORT : UDP
IP : 86.64.231.163
port serveur : 443
port local : 59914
``````
```````
youtube.com
PORT : UDP
IP : 142.250.178.138
Port serveur : 443
port local : 63676
``````````
``````````
crunchyroll.com
PORT : UDP
IP : 91.68.254.14
port serveur : 433
port local : 53036
``````````
``````
gmail.com
port : TCP
IP : 216.58.214.165
port serveur : 443
port local : 59957
``````
``````````
app.envoituresimone.com
port : TCP
IP : 172.217.20.206
port serveur : 433
port local : 60015
``````````
🌞 Demandez l'avis à votre OS

``````
PS C:\windows\system32> netstat -a -n -b

Connexions actives

Proto  Adresse locale         Adresse distante       État
TCP    0.0.0.0:135            0.0.0.0:0              LISTENING
RpcEptMapper
[svchost.exe]
TCP    0.0.0.0:445            0.0.0.0:0              LISTENING
Impossible d’obtenir les informations de propriétaire
TCP    0.0.0.0:902            0.0.0.0:0              LISTENING
[vmware-authd.exe]
TCP    0.0.0.0:912            0.0.0.0:0              LISTENING
[vmware-authd.exe]
TCP    0.0.0.0:5040           0.0.0.0:0              LISTENING
CDPSvc
[svchost.exe]
TCP    0.0.0.0:49664          0.0.0.0:0              LISTENING
[lsass.exe]
TCP    0.0.0.0:49665          0.0.0.0:0              LISTENING
Impossible d’obtenir les informations de propriétaire
TCP    0.0.0.0:49666          0.0.0.0:0              LISTENING
Schedule
[svchost.exe]
TCP    0.0.0.0:49667          0.0.0.0:0              LISTENING
EventLog
[svchost.exe]
TCP    0.0.0.0:49668          0.0.0.0:0              LISTENING
[spoolsv.exe]
TCP    0.0.0.0:49672          0.0.0.0:0              LISTENING
Impossible d’obtenir les informations de propriétaire
TCP    0.0.0.0:49733          0.0.0.0:0              LISTENING
[Spotify.exe]
TCP    0.0.0.0:57621          0.0.0.0:0              LISTENING
[Spotify.exe]
TCP    10.4.1.1:139           0.0.0.0:0              LISTENING
Impossible d’obtenir les informations de propriétaire
TCP    127.0.0.1:2021         0.0.0.0:0              LISTENING
[ExpressVPN.SystemService.exe]
TCP    127.0.0.1:2021         127.0.0.1:49673        ESTABLISHED
[ExpressVPN.SystemService.exe]
TCP    127.0.0.1:2022         0.0.0.0:0              LISTENING
[ExpressVPN.VpnService.exe]
TCP    127.0.0.1:2022         127.0.0.1:49675        ESTABLISHED
[ExpressVPN.VpnService.exe]
TCP    127.0.0.1:15292        0.0.0.0:0              LISTENING
[Adobe Desktop Service.exe]
TCP    127.0.0.1:15393        0.0.0.0:0              LISTENING
[Adobe Desktop Service.exe]
TCP    127.0.0.1:16494        0.0.0.0:0              LISTENING
[Adobe Desktop Service.exe]
TCP    127.0.0.1:27015        0.0.0.0:0              LISTENING
[AppleMobileDeviceService.exe]
TCP    127.0.0.1:45623        0.0.0.0:0              LISTENING
[node.exe]
TCP    127.0.0.1:49673        127.0.0.1:2021         ESTABLISHED
[ExpressVPN.AppService.exe]
TCP    127.0.0.1:49675        127.0.0.1:2022         ESTABLISHED
[ExpressVPN.AppService.exe]
TCP    127.0.0.1:49677        0.0.0.0:0              LISTENING
[ExpressVPN.AppService.exe]
TCP    127.0.0.1:49678        0.0.0.0:0              LISTENING
[AdskIdentityManager.exe]
TCP    127.0.0.1:49678        127.0.0.1:51830        ESTABLISHED
[AdskIdentityManager.exe]
TCP    127.0.0.1:49679        0.0.0.0:0              LISTENING
[AdskIdentityManager.exe]
TCP    127.0.0.1:49679        127.0.0.1:49681        ESTABLISHED
[AdskIdentityManager.exe]
TCP    127.0.0.1:49681        127.0.0.1:49679        ESTABLISHED
[AdskAccessCore.exe]
TCP    127.0.0.1:49926        0.0.0.0:0              LISTENING
[node.exe]
TCP    127.0.0.1:49927        0.0.0.0:0              LISTENING
[node.exe]
TCP    127.0.0.1:51788        127.0.0.1:49678        TIME_WAIT
TCP    127.0.0.1:51805        127.0.0.1:49678        TIME_WAIT
TCP    127.0.0.1:51814        127.0.0.1:49678        TIME_WAIT
TCP    127.0.0.1:51820        127.0.0.1:49678        TIME_WAIT
TCP    127.0.0.1:51830        127.0.0.1:49678        ESTABLISHED
[AdskAccessCore.exe]
TCP    127.0.0.1:56297        0.0.0.0:0              LISTENING
[AdskLicensingService.exe]
TCP    127.0.0.1:57402        0.0.0.0:0              LISTENING
[node.exe]
TCP    172.20.10.5:139        0.0.0.0:0              LISTENING
Impossible d’obtenir les informations de propriétaire
TCP    172.20.10.5:49410      20.199.120.85:443      ESTABLISHED
WpnService
[svchost.exe]
TCP    172.20.10.5:49411      20.199.120.85:443      ESTABLISHED
WpnService
[svchost.exe]
TCP    172.20.10.5:49734      104.199.65.124:4070    ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:49754      34.149.154.214:443     ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:49756      34.111.115.192:443     ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:50219      20.250.77.142:443      ESTABLISHED
[msedge.exe]
TCP    172.20.10.5:50372      13.69.109.130:443      ESTABLISHED
[Code.exe]
TCP    172.20.10.5:50914      34.232.214.120:443     ESTABLISHED
[CoreSync.exe]
TCP    172.20.10.5:50962      20.42.65.89:443        ESTABLISHED
[msedge.exe]
TCP    172.20.10.5:51339      140.82.112.25:443      ESTABLISHED
[msedge.exe]
TCP    172.20.10.5:51365      15.197.213.252:443     ESTABLISHED
[ExpressVPN.AppService.exe]
TCP    172.20.10.5:51676      213.155.157.147:443    ESTABLISHED
[msedge.exe]
TCP    172.20.10.5:51694      172.217.20.194:443     ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:51695      172.217.20.194:443     ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:51696      142.250.179.66:443     ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:51697      142.250.178.129:443    ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:51698      172.217.20.162:443     ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:51699      142.250.75.225:443     ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:51700      142.250.179.66:443     ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:51701      35.186.224.25:443      ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:51702      92.122.166.164:443     TIME_WAIT
TCP    172.20.10.5:51703      35.186.224.18:443      ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:51716      172.65.251.78:443      ESTABLISHED
[msedge.exe]
TCP    172.20.10.5:51739      172.64.147.68:443      ESTABLISHED
[msedge.exe]
TCP    172.20.10.5:51741      172.65.251.78:443      ESTABLISHED
[msedge.exe]
TCP    172.20.10.5:51779      140.82.121.3:443       ESTABLISHED
[msedge.exe]
TCP    172.20.10.5:51791      140.82.121.6:443       ESTABLISHED
[msedge.exe]
TCP    172.20.10.5:51796      140.82.113.21:443      ESTABLISHED
[msedge.exe]
TCP    172.20.10.5:51806      92.122.166.218:80      TIME_WAIT
TCP    172.20.10.5:51813      92.122.166.214:80      TIME_WAIT
TCP    172.20.10.5:51817      35.186.224.18:443      ESTABLISHED
[Spotify.exe]
TCP    172.20.10.5:51823      185.199.111.154:443    ESTABLISHED
[msedge.exe]
TCP    172.20.10.5:51829      92.122.166.218:80      TIME_WAIT
TCP    192.168.91.1:139       0.0.0.0:0              LISTENING
Impossible d’obtenir les informations de propriétaire
TCP    192.168.148.1:139      0.0.0.0:0              LISTENING
Impossible d’obtenir les informations de propriétaire
TCP    192.168.237.1:139      0.0.0.0:0              LISTENING
Impossible d’obtenir les informations de propriétaire
TCP    [::]:135               [::]:0                 LISTENING
RpcEptMapper
[svchost.exe]
TCP    [::]:445               [::]:0                 LISTENING
Impossible d’obtenir les informations de propriétaire
TCP    [::]:49664             [::]:0                 LISTENING
[lsass.exe]
TCP    [::]:49665             [::]:0                 LISTENING
Impossible d’obtenir les informations de propriétaire
TCP    [::]:49666             [::]:0                 LISTENING
Schedule
[svchost.exe]
TCP    [::]:49667             [::]:0                 LISTENING
EventLog
[svchost.exe]
TCP    [::]:49668             [::]:0                 LISTENING
[spoolsv.exe]
TCP    [::]:49672             [::]:0                 LISTENING
Impossible d’obtenir les informations de propriétaire
UDP    0.0.0.0:500            *:*
IKEEXT
[svchost.exe]
UDP    0.0.0.0:1900           *:*
[Spotify.exe]
UDP    0.0.0.0:1900           *:*
[Spotify.exe]
UDP    0.0.0.0:1900           *:*
[Spotify.exe]
UDP    0.0.0.0:1900           *:*
[Spotify.exe]
UDP    0.0.0.0:1900           *:*
[Spotify.exe]
UDP    0.0.0.0:4500           *:*
IKEEXT
[svchost.exe]
UDP    0.0.0.0:5050           *:*
CDPSvc
[svchost.exe]
UDP    0.0.0.0:5353           *:*
[msedge.exe]
UDP    0.0.0.0:5353           *:*
[msedge.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[msedge.exe]
UDP    0.0.0.0:5353           *:*
[msedge.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[msedge.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[msedge.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[msedge.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[msedge.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
Dnscache
[svchost.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[msedge.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[msedge.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5353           *:*
[Spotify.exe]
UDP    0.0.0.0:5355           *:*
Dnscache
[svchost.exe]
UDP    0.0.0.0:57238          *:*
Dnscache
[svchost.exe]
UDP    0.0.0.0:57621          *:*
[Spotify.exe]
UDP    0.0.0.0:63254          *:*
[Spotify.exe]
UDP    0.0.0.0:63255          *:*
[Spotify.exe]
UDP    0.0.0.0:63256          *:*
[Spotify.exe]
UDP    0.0.0.0:63257          *:*
[Spotify.exe]
UDP    0.0.0.0:63258          *:*
[Spotify.exe]
UDP    10.4.1.1:137           *:*
Impossible d’obtenir les informations de propriétaire
UDP    10.4.1.1:138           *:*
Impossible d’obtenir les informations de propriétaire
UDP    10.4.1.1:1900          *:*
SSDPSRV
[svchost.exe]
UDP    10.4.1.1:50793         *:*
SSDPSRV
[svchost.exe]
UDP    127.0.0.1:1900         *:*
SSDPSRV
[svchost.exe]
UDP    127.0.0.1:50797        *:*
SSDPSRV
[svchost.exe]
UDP    127.0.0.1:65364        127.0.0.1:65365
[AppleMobileDeviceService.exe]
UDP    127.0.0.1:65365        127.0.0.1:65364
[AppleMobileDeviceService.exe]
UDP    127.0.0.1:65366        127.0.0.1:65366
iphlpsvc
[svchost.exe]
UDP    172.20.10.5:137        *:*
Impossible d’obtenir les informations de propriétaire
UDP    172.20.10.5:138        *:*
Impossible d’obtenir les informations de propriétaire
UDP    172.20.10.5:1900       *:*
SSDPSRV
[svchost.exe]
UDP    172.20.10.5:50792      *:*
SSDPSRV
[svchost.exe]
UDP    192.168.91.1:137       *:*
Impossible d’obtenir les informations de propriétaire
UDP    192.168.91.1:138       *:*
Impossible d’obtenir les informations de propriétaire
UDP    192.168.91.1:1900      *:*
SSDPSRV
[svchost.exe]
UDP    192.168.91.1:50795     *:*
SSDPSRV
[svchost.exe]
UDP    192.168.148.1:137      *:*
Impossible d’obtenir les informations de propriétaire
UDP    192.168.148.1:138      *:*
Impossible d’obtenir les informations de propriétaire
UDP    192.168.148.1:1900     *:*
SSDPSRV
[svchost.exe]
UDP    192.168.148.1:50794    *:*
SSDPSRV
[svchost.exe]
UDP    192.168.237.1:137      *:*
Impossible d’obtenir les informations de propriétaire
UDP    192.168.237.1:138      *:*
Impossible d’obtenir les informations de propriétaire
UDP    192.168.237.1:1900     *:*
SSDPSRV
[svchost.exe]
UDP    192.168.237.1:50796    *:*
SSDPSRV
[svchost.exe]
UDP    [::]:500               *:*
IKEEXT
[svchost.exe]
UDP    [::]:4500              *:*
IKEEXT
[svchost.exe]
UDP    [::]:5353              *:*
[Spotify.exe]
UDP    [::]:5353              *:*
[Spotify.exe]
UDP    [::]:5353              *:*
[Spotify.exe]
UDP    [::]:5353              *:*
[Spotify.exe]
UDP    [::]:5353              *:*
[Spotify.exe]
UDP    [::]:5353              *:*
[Spotify.exe]
UDP    [::]:5353              *:*
[msedge.exe]
UDP    [::]:5353              *:*
[msedge.exe]
UDP    [::]:5353              *:*
[msedge.exe]
UDP    [::]:5353              *:*
[Spotify.exe]
UDP    [::]:5353              *:*
[msedge.exe]
UDP    [::]:5353              *:*
[msedge.exe]
UDP    [::]:5353              *:*
[Spotify.exe]
UDP    [::]:5353              *:*
[Spotify.exe]
UDP    [::]:5353              *:*
[Spotify.exe]
UDP    [::]:5353              *:*
Dnscache
[svchost.exe]
UDP    [::]:5355              *:*
Dnscache
[svchost.exe]
UDP    [::]:57238             *:*
Dnscache
[svchost.exe]
UDP    [::1]:1900             *:*
SSDPSRV
[svchost.exe]
UDP    [::1]:50791            *:*
SSDPSRV
[svchost.exe]
UDP    [fe80::337a:1361:ea83:2cc%24]:1900  *:*
SSDPSRV
[svchost.exe]
UDP    [fe80::337a:1361:ea83:2cc%24]:50789  *:*
SSDPSRV
[svchost.exe]
UDP    [fe80::4135:70b9:32e7:7b7%21]:1900  *:*
SSDPSRV
[svchost.exe]
UDP    [fe80::4135:70b9:32e7:7b7%21]:50787  *:*
SSDPSRV
[svchost.exe]
UDP    [fe80::4dfa:3e92:bbf:6ffa%18]:1900  *:*
SSDPSRV
[svchost.exe]
UDP    [fe80::4dfa:3e92:bbf:6ffa%18]:50786  *:*
SSDPSRV
[svchost.exe]
UDP    [fe80::8c98:2077:8f31:ae90%17]:1900  *:*
SSDPSRV
[svchost.exe]
UDP    [fe80::8c98:2077:8f31:ae90%17]:50788  *:*
SSDPSRV
[svchost.exe]
UDP    [fe80::b5e9:fd4b:53ca:a8f8%13]:1900  *:*
SSDPSRV
[svchost.exe]
UDP    [fe80::b5e9:fd4b:53ca:a8f8%13]:50790  *:*
SSDPSRV
[svchost.exe]
``````````
