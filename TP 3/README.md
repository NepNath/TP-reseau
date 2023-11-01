# TP-reseau-3 : On va router des trucs

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

### 🌞Analyse de trames

