# TP-reseau-3 : On va router des trucs
bon vu que je suis un golmon et que je relis mes trucs 20 ans après il se peut que y'a des aberations dans mes réponses ou des grosses incoréhences (je relis a la fin et vu que entre temps j'ai capté 245625 trucs que j'avais pas compris au début bah voilà) (niveau commande, addr MAC ou autre) <br>

aussi parce que ça rend le truc plus simple a lire les informations importantes seront noté entre 👉 **info de fou**👈 et a côté des commandes y'aura un ptit 💻

# I. ARP
## 1. Echange ARP
### 🌞Générer des requêtes ARP
* récupérer l'adresse MAC de `john` dans la table arp de `marcel` et vice versa :
``` 
[nepnath@john ~]$ ip n s 💻
10.3.1.1 dev enp0s3 lladdr 👉0a:00:27:00:00:0e👈 DELAY
10.3.1.254 dev enp0s3 lladdr 👉08:00:27:2e:90:ef👈 REACHABLE
```
[nepnath@marcel ~]$ ip n s 💻
10.3.2.254 dev enp0s3 lladdr 👉08:00:27:c2:cc:8d👈 STALE
10.3.2.1 dev enp0s3 lladdr 👉0a:00:27:00:00:16👈 DELAY


* prouvez que l'adresse est correcte 
``` 
[nepnath@marcel ~]$ ip a 💻
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 👉08:00:27:e1:64:b8👈
```
```
[nepnath@john ~]$ ip a 💻
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 👉08:00:27:6e:49:86👈
``` 


## 2. Analyse de trames

`ip neigh flush all ` 💻 pour vider la table arp <br>

### 🌞🦈Analyse de trames
normalement le fichier se trouve dans [ce dossier](!https://github.com/NepNath/TP-reseau-1/tree/main/TP%203/External%20files) sous le nom de <ins>**super-fichier.pcapng**</ins> <br>

# II Routage 

### 🌞Ajouter les routes statiques nécessaires pour que john et marcel puissent se ping

set des routes : 
```
[nepnath@john ~]$ cat /etc/sysconfig/network-scripts/route-enp0s3 💻
👉10.3.2.0/24 via 10.3.1.254 dev enp0s3👈 
👉default via 10.3.2.254 dev enp0s3👈
```

```
[nepnath@marcel ~]$ cat /etc/sysconfig/network-scripts/route-enp0s3 💻
👉10.3.1.0/24 via 10.3.2.254 dev enp0s3👈 
👉default via 10.3.2.254 dev enp0s3👈 (permet de faire une route globale (genre crée une route vers partout a la ou c'est connecté via 10.3.2.254))
```


depuis john (10.3.1.11) : 

`[nepnath@localhost network-scripts]$ ping 10.3.2.12`<br>
`PING 10.3.2.12 (10.3.2.12) 56(84) bytes of data.`<br>
`64 bytes from 10.3.2.12: icmp_seq=1 ttl=63 time=2.20 ms`<br>
`64 bytes from 10.3.2.12: icmp_seq=2 ttl=63 time=1.68 ms`<br>
`64 bytes from 10.3.2.12: icmp_seq=3 ttl=63 time=1.94 ms`<br>

depuis marcel (10.3.2.12): 

`[nepnath@localhost network-scripts]$ ping 10.3.1.11`<br>
`PING 10.3.1.11 (10.3.1.11) 56(84) bytes of data.`<br>
`64 bytes from 10.3.1.11: icmp_seq=1 ttl=63 time=2.58 ms`<br>
`64 bytes from 10.3.1.11: icmp_seq=2 ttl=63 time=1.83 ms`<br>
`64 bytes from 10.3.1.11: icmp_seq=3 ttl=63 time=1.44 ms`<br>
`64 bytes from 10.3.1.11: icmp_seq=4 ttl=63 time=2.42 ms`<br>

| Ordre | type tramme | IP source | MAC source | IP destination | MAC destination | 
--- | --- | --- | --- | --- | ---
1 | requête ARP | X | Marcel `08:00:27:e1:64:b8` | X | Broadcast `ff:ff:ff:ff:ff:ff`
2 | réponse ARP | X | John `08:00:27:6e:49:86` | X | Marcel `08:00:27:e1:64:b8`
... | ... | ... | ... | ... | ...
4 | Ping | Marcel `10.3.2.12` | Marcel `08:00:27:e1:64:b8` | john `10.3.1.11` | John `08:00:27:6e:49:86`
5 | pong | John `10.3.1.11` | John `08:00:27:6e:49:86` | Marcel `10.3.2.12` | Marcel `08:00:27:e1:64:b8`

### 🌞Donnez un accès internet à vos machines

* **routes** : 
```
[nepnath@john network-scripts]$ sudo cat /etc/sysconfig/network-scripts/route-enp0s3
10.3.2.0/24 via 10.3.1.254 dev enp0s3
default via 10.3.1.254 dev enp0s3
```
```
[nepnath@marcel ~]$ sudo cat /etc/sysconfig/network-scripts/route-enp0s3
10.3.1.0/24 via 10.3.2.254 dev enp0s3
default via 10.3.2.254 dev enp0s3
```

* **ping d'ip**

```
[nepnath@john ~]$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=115 time=11.2 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=115 time=11.4 ms
```

```
[nepnath@marcel ~]$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=115 time=11.3 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=115 time=11.6 ms
```

* **ping de nom de domaine**

```
[nepnath@john ~]$ ping google.com
PING google.com (172.217.20.206) 56(84) bytes of data.
64 bytes from waw02s08-in-f14.1e100.net (172.217.20.206): icmp_seq=1 ttl=115 time=11.1 ms
64 bytes from par10s50-in-f14.1e100.net (172.217.20.206): icmp_seq=2 ttl=115 time=10.9 ms
^C
--- google.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 10.942/11.042/11.143/0.100 ms
```

```
[nepnath@marcel ~]$ ping google.com
PING google.com (142.250.179.110) 56(84) bytes of data.
64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=1 ttl=114 time=11.5 ms
64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=2 ttl=114 time=11.4 ms
^C
--- google.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 11.423/11.472/11.522/0.049 ms
[nepnath@marcel ~]$
```