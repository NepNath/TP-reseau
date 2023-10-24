# TP-reseau-3 : On va router des trucs

## 1. Echange ARP
### 🌞Générer des requêtes ARP
* récupérer l'adresse MAC de `john` dans la table arp de `marcel` et vice versa : 
> commande = `ip neight` <br>
résultat depuis john =  `10.3.1.12 dev enp0s3 lladdr 08:00:27:e1:64:b8 STALE` <-- Adresse de marcel <br>
résultat depuis marcel =  `10.3.1.11 dev enp0s3 lladdr 08:00:27:6e:49:86 STALE` <-- Adresse de john

* prouvez que l'adresse est correcte 

> commande = `ip a` (dans les deux serveurs) <br>
résultat de john = `link/ether 08:00:27:6e:49:86` <br>
résultat de marcel = `link/ether 08:00:27:e1:64:b8 brd` <br>

## 2. Analyse de trames

### 🌞Analyse de trames

