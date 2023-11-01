# TP2 : Ethernet, IP, et ARP


## I. Setup IP

### 🌞 Mettez en place une configuration réseau fonctionnelle entre les deux machines

**commmande :** `ping 10.3.1.12` (j'avais cette VM d'allumée sous la main faut pas faire gaffe a l'ip) <br>

**résultat :** <br> 
`Envoi d’une requête 'Ping'  10.3.1.12 avec 32 octets de données :` <br>
`Réponse de 10.3.1.12 : octets=32 temps=2 ms TTL=64` <br>
`Réponse de 10.3.1.12 : octets=32 temps<1ms TTL=64` <br>
`Réponse de 10.3.1.12 : octets=32 temps<1ms TTL=64`   <br>
`Réponse de 10.3.1.12 : octets=32 temps<1ms TTL=64` <br>

### 🌞 Wireshark it

🦈 **fichier trouvable dans [ce dossier](https://github.com/NepNath/TP-reseau-1/tree/main/TP%202/External%20files) sous le nom de <ins>TP2-WiresharkIt.pcap</ins>**

## II. ARP my bro

mon binome étant une superbe VM je peux check son adresse MAC comme ça : 

**commande :** 
<br>`arp -a` (windows)<br>
`ip neigh show` (linux) <br>

et le **résultat** est le suivant (sur windows) : <br>
`Interface : 10.3.1.1 --- 0xd` <br>
    `10.3.1.12.......08-00-27-e1-64-b8......dynamique` <br>
<br>

`Interface : 192.168.1.64 --- 0x8`<br>
  `192.168.1.1......48-29-52-0a-a9-b0......dynamique`

