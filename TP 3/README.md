# TP-reseau-3 : On va router des trucs

# I. ARP
## 1. Echange ARP
### 🌞Générer des requêtes ARP
* récupérer l'adresse MAC de `john` dans la table arp de `marcel` et vice versa : 
> commande = `ip neight show` <br>
résultat : <br>`[nepnath@localhost ~]$ ip neigh show` <br>
`10.3.1.1 dev enp0s3 lladdr 0a:00:27:00:00:0d DELAY` <br>
`10.3.1.12 dev enp0s3 lladdr 08:00:27:e1:64:b8 STALE`<br>
<br>
`[nepnath@localhost ~]$ ip neigh` <br>
`10.3.1.11 dev enp0s3 lladdr 08:00:27:6e:49:86 STALE` <br>
`10.3.1.1 dev enp0s3 lladdr 0a:00:27:00:00:0d REACHABLE` <br>

* prouvez que l'adresse est correcte 

> commande = `ip a` (dans les deux serveurs) <br>
résultat de 10.3.1.12 = `08:00:27:e1:64:b8` <br>
résultat de 10.3.1.11 = `08:00:27:6e:49:86` <br>
    
## 2. Analyse de trames


### 🌞🦈Analyse de trames
normalement le fichier se trouve dans [ce dossier](!https://github.com/NepNath/TP-reseau-1/tree/main/TP%203/External%20files) sous le nom de <ins>**super-fichier.pcapng**</ins> <br>

# II Routage 

### 🌞Ajouter les routes statiques nécessaires pour que john et marcel puissent se ping
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