# Tarefa 1.3
---
## 1 Ficheros de configuración e log dos equipos vendo a transferencia
### 1.1 Ficheros de configuracion (named.conf.local)
#### 1.1.1 Servidor primario 
```
zone "starwars.lan" IN {
    type master;
    file "/etc/bind/db.starwars.lan";
    allow-transfer {192.168.20.11;};
    notify yes;
};
zone "20.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/db.20.168.192";
    allow-transfer {192.168.20.11;};
    notify yes;
};
```
#### 1.1.2 Servidor secundario
```
zone "starwars.lan" IN {
    type slave;
    file "/etc/bind/db.starwars.lan";
    masters {192.168.20.100;};
};
zone "20.168.192.in-addr.arpa" {
    type slave;
    file "/etc/bind/db.20.168.192";
    masters {192.168.20.100;};
};
```
### 1.2 Logs
```
a24lucasba@a24eql13:~/SRI/Tarefa1.3$ dc logs dnsserver
dnsserver-1  | Starting domain name service...: named.
dnsserver-1  | 2025-11-05T08:08:00.170507+00:00 dnsserver named[19]: command channel listening on ::1#953
dnsserver-1  | 2025-11-05T08:08:00.171828+00:00 dnsserver named[19]: managed-keys-zone: loaded serial 0
dnsserver-1  | 2025-11-05T08:08:00.174479+00:00 dnsserver named[19]: zone 0.in-addr.arpa/IN: loaded serial 1
dnsserver-1  | 2025-11-05T08:08:00.174833+00:00 dnsserver named[19]: zone 127.in-addr.arpa/IN: loaded serial 1
dnsserver-1  | 2025-11-05T08:08:00.180500+00:00 dnsserver named[19]: zone starwars.lan/IN: loaded serial 1
dnsserver-1  | 2025-11-05T08:08:00.180861+00:00 dnsserver named[19]: zone 20.168.192.in-addr.arpa/IN: loaded serial 1
dnsserver-1  | 2025-11-05T08:08:00.182720+00:00 dnsserver named[19]: zone 255.in-addr.arpa/IN: loaded serial 1
dnsserver-1  | 2025-11-05T08:08:00.184249+00:00 dnsserver named[19]: zone localhost/IN: loaded serial 2
dnsserver-1  | 2025-11-05T08:08:00.184411+00:00 dnsserver named[19]: all zones loaded
dnsserver-1  | 2025-11-05T08:08:00.184681+00:00 dnsserver named[19]: running
dnsserver-1  | 2025-11-05T08:08:00.429093+00:00 dnsserver named[19]: client @0x734fdac19c98 192.168.20.11#37209 (20.168.192.in-addr.arpa): transfer of '20.168.192.in-addr.arpa/IN': AXFR started (serial 1)
dnsserver-1  | 2025-11-05T08:08:00.429313+00:00 dnsserver named[19]: client @0x734fdac19c98 192.168.20.11#37209 (20.168.192.in-addr.arpa): transfer of '20.168.192.in-addr.arpa/IN': AXFR ended: 1 messages, 11 records, 332 bytes, 0.001 secs (332000 bytes/sec) (serial 1)
dnsserver-1  | 2025-11-05T08:08:00.929274+00:00 dnsserver named[19]: client @0x734fc7a19c98 192.168.20.11#37735 (starwars.lan): transfer of 'starwars.lan/IN': AXFR started (serial 1)
dnsserver-1  | 2025-11-05T08:08:00.929507+00:00 dnsserver named[19]: client @0x734fc7a19c98 192.168.20.11#37735 (starwars.lan): transfer of 'starwars.lan/IN': AXFR ended: 1 messages, 15 records, 398 bytes, 0.001 secs (398000 bytes/sec) (serial 1)
dnsserver-1  | 2025-11-05T08:08:01.041528+00:00 dnsserver rsyslogd: [origin software="rsyslogd" swVersion="8.2302.0" x-pid="9" x-info="https://www.rsyslog.com"] start
```
```
a24lucasba@a24eql13:~/SRI/Tarefa1.3$ dc logs dnsserver2
dnsserver2-1  | Starting domain name service...: named.
dnsserver2-1  | 2025-11-05T08:08:00.422982+00:00 darthsidious named[19]: zone localhost/IN: loaded serial 2
dnsserver2-1  | 2025-11-05T08:08:00.427275+00:00 darthsidious named[19]: zone 255.in-addr.arpa/IN: loaded serial 1
dnsserver2-1  | 2025-11-05T08:08:00.427428+00:00 darthsidious named[19]: all zones loaded
dnsserver2-1  | 2025-11-05T08:08:00.427758+00:00 darthsidious named[19]: running
dnsserver2-1  | 2025-11-05T08:08:00.428219+00:00 darthsidious named[19]: zone 20.168.192.in-addr.arpa/IN: Transfer started.
dnsserver2-1  | 2025-11-05T08:08:00.428415+00:00 darthsidious named[19]: transfer of '20.168.192.in-addr.arpa/IN' from 192.168.20.100#53: connected using 192.168.20.100#53
dnsserver2-1  | 2025-11-05T08:08:00.429492+00:00 darthsidious named[19]: zone 20.168.192.in-addr.arpa/IN: transferred serial 1
dnsserver2-1  | 2025-11-05T08:08:00.429544+00:00 darthsidious named[19]: transfer of '20.168.192.in-addr.arpa/IN' from 192.168.20.100#53: Transfer status: success
dnsserver2-1  | 2025-11-05T08:08:00.429562+00:00 darthsidious named[19]: transfer of '20.168.192.in-addr.arpa/IN' from 192.168.20.100#53: Transfer completed: 1 messages, 11 records, 332 bytes, 0.001 secs (332000 bytes/sec) (serial 1)
dnsserver2-1  | 2025-11-05T08:08:00.429760+00:00 darthsidious named[19]: dumping master file: /etc/bind/tmp-qfUXB7UWer: open: permission denied
dnsserver2-1  | 2025-11-05T08:08:00.928389+00:00 darthsidious named[19]: zone starwars.lan/IN: Transfer started.
dnsserver2-1  | 2025-11-05T08:08:00.928806+00:00 darthsidious named[19]: transfer of 'starwars.lan/IN' from 192.168.20.100#53: connected using 192.168.20.100#53
dnsserver2-1  | 2025-11-05T08:08:00.929914+00:00 darthsidious named[19]: zone starwars.lan/IN: transferred serial 1
dnsserver2-1  | 2025-11-05T08:08:00.929963+00:00 darthsidious named[19]: transfer of 'starwars.lan/IN' from 192.168.20.100#53: Transfer status: success
dnsserver2-1  | 2025-11-05T08:08:00.929974+00:00 darthsidious named[19]: transfer of 'starwars.lan/IN' from 192.168.20.100#53: Transfer completed: 1 messages, 15 records, 398 bytes, 0.001 secs (398000 bytes/sec) (serial 1)
dnsserver2-1  | 2025-11-05T08:08:00.930132+00:00 darthsidious named[19]: dumping master file: /etc/bind/tmp-4VPLhhBlHy: open: permission denied
dnsserver2-1  | 2025-11-05T08:08:01.253509+00:00 darthsidious rsyslogd: [origin software="rsyslogd" swVersion="8.2302.0" x-pid="9" x-info="https://www.rsyslog.com"] start
```
---
## 2 Agregar o rexistro tipo A Chewbacca 192.168.20.28 e comprobar os logs
```
a24lucasba@a24eql13:~/SRI/Tarefa1.3$ dc logs dnsserver
dnsserver-1  | Starting domain name service...: named.
dnsserver-1  | 2025-11-05T08:40:42.518333+00:00 dnsserver named[19]: command channel listening on ::1#953
dnsserver-1  | 2025-11-05T08:40:42.519941+00:00 dnsserver named[19]: managed-keys-zone: loaded serial 0
dnsserver-1  | 2025-11-05T08:40:42.520913+00:00 dnsserver named[19]: zone 0.in-addr.arpa/IN: loaded serial 1
dnsserver-1  | 2025-11-05T08:40:42.524773+00:00 dnsserver named[19]: zone 127.in-addr.arpa/IN: loaded serial 1
dnsserver-1  | 2025-11-05T08:40:42.526084+00:00 dnsserver named[19]: zone starwars.lan/IN: loaded serial 1
dnsserver-1  | 2025-11-05T08:40:42.530229+00:00 dnsserver named[19]: zone 255.in-addr.arpa/IN: loaded serial 1
dnsserver-1  | 2025-11-05T08:40:42.531118+00:00 dnsserver named[19]: zone localhost/IN: loaded serial 2
dnsserver-1  | 2025-11-05T08:40:42.531423+00:00 dnsserver named[19]: zone 20.168.192.in-addr.arpa/IN: loaded serial 1
dnsserver-1  | 2025-11-05T08:40:42.533120+00:00 dnsserver named[19]: all zones loaded
dnsserver-1  | 2025-11-05T08:40:42.533374+00:00 dnsserver named[19]: running
dnsserver-1  | 2025-11-05T08:40:42.763171+00:00 dnsserver named[19]: client @0x74d5b4e19c98 192.168.20.11#43095 (starwars.lan): transfer of 'starwars.lan/IN': AXFR started (serial 1)
dnsserver-1  | 2025-11-05T08:40:42.763388+00:00 dnsserver named[19]: client @0x74d5b4e19c98 192.168.20.11#43095 (starwars.lan): transfer of 'starwars.lan/IN': AXFR ended: 1 messages, 16 records, 424 bytes, 0.001 secs (424000 bytes/sec) (serial 1)
dnsserver-1  | 2025-11-05T08:40:43.263072+00:00 dnsserver named[19]: client @0x74d5b8219c98 192.168.20.11#40319 (20.168.192.in-addr.arpa): transfer of '20.168.192.in-addr.arpa/IN': AXFR started (serial 1)
dnsserver-1  | 2025-11-05T08:40:43.263323+00:00 dnsserver named[19]: client @0x74d5b8219c98 192.168.20.11#40319 (20.168.192.in-addr.arpa): transfer of '20.168.192.in-addr.arpa/IN': AXFR ended: 1 messages, 12 records, 359 bytes, 0.001 secs (359000 bytes/sec) (serial 1)
dnsserver-1  | 2025-11-05T08:40:43.365776+00:00 dnsserver rsyslogd: [origin software="rsyslogd" swVersion="8.2302.0" x-pid="9" x-info="https://www.rsyslog.com"] start
```
```
a24lucasba@a24eql13:~/SRI/Tarefa1.3$ dc logs dnsserver2
dnsserver2-1  | Starting domain name service...: named.
dnsserver2-1  | 2025-11-05T08:40:42.755150+00:00 darthsidious named[19]: zone localhost/IN: loaded serial 2
dnsserver2-1  | 2025-11-05T08:40:42.756319+00:00 darthsidious named[19]: zone 255.in-addr.arpa/IN: loaded serial 1
dnsserver2-1  | 2025-11-05T08:40:42.761198+00:00 darthsidious named[19]: all zones loaded
dnsserver2-1  | 2025-11-05T08:40:42.761457+00:00 darthsidious named[19]: running
dnsserver2-1  | 2025-11-05T08:40:42.762436+00:00 darthsidious named[19]: zone starwars.lan/IN: Transfer started.
dnsserver2-1  | 2025-11-05T08:40:42.762720+00:00 darthsidious named[19]: transfer of 'starwars.lan/IN' from 192.168.20.100#53: connected using 192.168.20.100#53
dnsserver2-1  | 2025-11-05T08:40:42.763536+00:00 darthsidious named[19]: zone starwars.lan/IN: transferred serial 1
dnsserver2-1  | 2025-11-05T08:40:42.763580+00:00 darthsidious named[19]: transfer of 'starwars.lan/IN' from 192.168.20.100#53: Transfer status: success
dnsserver2-1  | 2025-11-05T08:40:42.763592+00:00 darthsidious named[19]: transfer of 'starwars.lan/IN' from 192.168.20.100#53: Transfer completed: 1 messages, 16 records, 424 bytes, 0.001 secs (424000 bytes/sec) (serial 1)
dnsserver2-1  | 2025-11-05T08:40:42.763739+00:00 darthsidious named[19]: dumping master file: /etc/bind/tmp-3BT7Uti7hG: open: permission denied
dnsserver2-1  | 2025-11-05T08:40:43.262174+00:00 darthsidious named[19]: zone 20.168.192.in-addr.arpa/IN: Transfer started.
dnsserver2-1  | 2025-11-05T08:40:43.262423+00:00 darthsidious named[19]: transfer of '20.168.192.in-addr.arpa/IN' from 192.168.20.100#53: connected using 192.168.20.100#53
dnsserver2-1  | 2025-11-05T08:40:43.263600+00:00 darthsidious named[19]: zone 20.168.192.in-addr.arpa/IN: transferred serial 1
dnsserver2-1  | 2025-11-05T08:40:43.263691+00:00 darthsidious named[19]: transfer of '20.168.192.in-addr.arpa/IN' from 192.168.20.100#53: Transfer status: success
dnsserver2-1  | 2025-11-05T08:40:43.263704+00:00 darthsidious named[19]: transfer of '20.168.192.in-addr.arpa/IN' from 192.168.20.100#53: Transfer completed: 1 messages, 12 records, 359 bytes, 0.002 secs (179500 bytes/sec) (serial 1)
dnsserver2-1  | 2025-11-05T08:40:43.263877+00:00 darthsidious named[19]: dumping master file: /etc/bind/tmp-Rfi3X83eNT: open: permission denied
dnsserver2-1  | 2025-11-05T08:40:43.596160+00:00 darthsidious rsyslogd: [origin software="rsyslogd" swVersion="8.2302.0" x-pid="9" x-info="https://www.rsyslog.com"] start
```
## 3 Comprobar que o servidor secundario pode resolver ese nome
```
root@darthsidious:/# nslookup chewbacca.starwars.lan localhost    
Server:		localhost
Address:	127.0.0.1#53

Name:	chewbacca.starwars.lan
Address: 192.168.20.28

root@darthsidious:/# nslookup 192.168.20.28 localhost
28.20.168.192.in-addr.arpa	name = chewbacca.starwars.lan.
```
## 4 Hacer los cambios necesarios para que la conexion sea a través de una clave y añadir un nuevo registro r2d2 192.168.20.29
```
a24lucasba@a24eql13:~/SRI/Tarefa1.3$ dc logs dnsserver
dnsserver-1  | Starting domain name service...: named.
dnsserver-1  | 2025-11-05T09:06:57.112770+00:00 dnsserver named[19]: managed-keys-zone: loaded serial 0
dnsserver-1  | 2025-11-05T09:06:57.115890+00:00 dnsserver named[19]: zone 0.in-addr.arpa/IN: loaded serial 1
dnsserver-1  | 2025-11-05T09:06:57.121171+00:00 dnsserver named[19]: zone 255.in-addr.arpa/IN: loaded serial 1
dnsserver-1  | 2025-11-05T09:06:57.121930+00:00 dnsserver named[19]: /etc/bind/db.20.168.192:20: file does not end with newline
dnsserver-1  | 2025-11-05T09:06:57.122043+00:00 dnsserver named[19]: zone localhost/IN: loaded serial 2
dnsserver-1  | 2025-11-05T09:06:57.122158+00:00 dnsserver named[19]: zone 20.168.192.in-addr.arpa/IN: loaded serial 1
dnsserver-1  | 2025-11-05T09:06:57.123084+00:00 dnsserver named[19]: zone starwars.lan/IN: loaded serial 1
dnsserver-1  | 2025-11-05T09:06:57.123140+00:00 dnsserver named[19]: zone 127.in-addr.arpa/IN: loaded serial 1
dnsserver-1  | 2025-11-05T09:06:57.124936+00:00 dnsserver named[19]: all zones loaded
dnsserver-1  | 2025-11-05T09:06:57.125203+00:00 dnsserver named[19]: running
dnsserver-1  | 2025-11-05T09:06:57.356281+00:00 dnsserver named[19]: client @0x79a6e4e81c98 192.168.20.11#39109/key transfer-key (20.168.192.in-addr.arpa): transfer of '20.168.192.in-addr.arpa/IN': AXFR started: TSIG transfer-key (serial 1)
dnsserver-1  | 2025-11-05T09:06:57.356537+00:00 dnsserver named[19]: client @0x79a6e4e81c98 192.168.20.11#39109/key transfer-key (20.168.192.in-addr.arpa): transfer of '20.168.192.in-addr.arpa/IN': AXFR ended: 1 messages, 13 records, 466 bytes, 0.001 secs (466000 bytes/sec) (serial 1)
dnsserver-1  | 2025-11-05T09:06:57.857100+00:00 dnsserver named[19]: client @0x79a6e5698c98 192.168.20.11#43811/key transfer-key (starwars.lan): transfer of 'starwars.lan/IN': AXFR started: TSIG transfer-key (serial 1)
dnsserver-1  | 2025-11-05T09:06:57.857438+00:00 dnsserver named[19]: client @0x79a6e5698c98 192.168.20.11#43811/key transfer-key (starwars.lan): transfer of 'starwars.lan/IN': AXFR ended: 1 messages, 17 records, 530 bytes, 0.001 secs (530000 bytes/sec) (serial 1)
dnsserver-1  | 2025-11-05T09:06:57.966276+00:00 dnsserver rsyslogd: [origin software="rsyslogd" swVersion="8.2302.0" x-pid="9" x-info="https://www.rsyslog.com"] start
```
```
a24lucasba@a24eql13:~/SRI/Tarefa1.3$ dc logs dnsserver2
dnsserver2-1  | Starting domain name service...: named.
dnsserver2-1  | 2025-11-05T09:06:57.340491+00:00 darthsidious named[18]: command channel listening on ::1#953
dnsserver2-1  | 2025-11-05T09:06:57.341833+00:00 darthsidious named[18]: managed-keys-zone: loaded serial 0
dnsserver2-1  | 2025-11-05T09:06:57.343057+00:00 darthsidious named[18]: zone 0.in-addr.arpa/IN: loaded serial 1
dnsserver2-1  | 2025-11-05T09:06:57.347133+00:00 darthsidious named[18]: zone 255.in-addr.arpa/IN: loaded serial 1
dnsserver2-1  | 2025-11-05T09:06:57.347992+00:00 darthsidious named[18]: zone 127.in-addr.arpa/IN: loaded serial 1
dnsserver2-1  | 2025-11-05T09:06:57.350714+00:00 darthsidious named[18]: zone localhost/IN: loaded serial 2
dnsserver2-1  | 2025-11-05T09:06:57.354231+00:00 darthsidious named[18]: all zones loaded
dnsserver2-1  | 2025-11-05T09:06:57.354434+00:00 darthsidious named[18]: running
dnsserver2-1  | 2025-11-05T09:06:57.355661+00:00 darthsidious named[18]: zone 20.168.192.in-addr.arpa/IN: Transfer started.
dnsserver2-1  | 2025-11-05T09:06:57.355827+00:00 darthsidious named[18]: transfer of '20.168.192.in-addr.arpa/IN' from 192.168.20.100#53: connected using 192.168.20.100#53 TSIG transfer-key
dnsserver2-1  | 2025-11-05T09:06:57.356904+00:00 darthsidious named[18]: zone 20.168.192.in-addr.arpa/IN: transferred serial 1: TSIG 'transfer-key'
dnsserver2-1  | 2025-11-05T09:06:57.356944+00:00 darthsidious named[18]: transfer of '20.168.192.in-addr.arpa/IN' from 192.168.20.100#53: Transfer status: success
dnsserver2-1  | 2025-11-05T09:06:57.356954+00:00 darthsidious named[18]: transfer of '20.168.192.in-addr.arpa/IN' from 192.168.20.100#53: Transfer completed: 1 messages, 13 records, 466 bytes, 0.001 secs (466000 bytes/sec) (serial 1)
dnsserver2-1  | 2025-11-05T09:06:57.357078+00:00 darthsidious named[18]: dumping master file: /etc/bind/tmp-esrRQJQOld: open: permission denied
dnsserver2-1  | 2025-11-05T09:06:57.856167+00:00 darthsidious named[18]: zone starwars.lan/IN: Transfer started.
dnsserver2-1  | 2025-11-05T09:06:57.856526+00:00 darthsidious named[18]: transfer of 'starwars.lan/IN' from 192.168.20.100#53: connected using 192.168.20.100#53 TSIG transfer-key
dnsserver2-1  | 2025-11-05T09:06:57.857713+00:00 darthsidious named[18]: zone starwars.lan/IN: transferred serial 1: TSIG 'transfer-key'
dnsserver2-1  | 2025-11-05T09:06:57.857884+00:00 darthsidious named[18]: transfer of 'starwars.lan/IN' from 192.168.20.100#53: Transfer status: success
dnsserver2-1  | 2025-11-05T09:06:57.857908+00:00 darthsidious named[18]: transfer of 'starwars.lan/IN' from 192.168.20.100#53: Transfer completed: 1 messages, 17 records, 530 bytes, 0.002 secs (265000 bytes/sec) (serial 1)
dnsserver2-1  | 2025-11-05T09:06:57.858186+00:00 darthsidious named[18]: dumping master file: /etc/bind/tmp-DGnJwHlNlX: open: permission denied
dnsserver2-1  | 2025-11-05T09:06:58.189943+00:00 darthsidious rsyslogd: [origin software="rsyslogd" swVersion="8.2302.0" x-pid="8" x-info="https://www.rsyslog.com"] start

```