# I. DHCP Client:
 

### 🌞 Déterminer

PS C:\Users\ldnat> ipconfig /all 💻
```
Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : MediaTek Wi-Fi 6 MT7921 Wireless LAN Card
   Adresse physique . . . . . . . . . . . : 50-5A-65-4F-B8-61
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::5ff0:538a:f1e4:3674%9(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.70.170(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Bail obtenu. . . . . . . . . . . . . . : 👉vendredi 24 novembre 2023 09:12:37👈
   Bail expirant. . . . . . . . . . . . . : 👉samedi 25 novembre 2023 09:12:37👈
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
   Serveur DHCP . . . . . . . . . . . . . : 👉10.33.79.254👈
   IAID DHCPv6 . . . . . . . . . . . : 105929317
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2B-A6-13-81-A0-36-BC-6B-C2-E1
   Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                       1.1.1.1
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé
   ```

### 🌞 Capturer un échange DHCP

le fichier est trouvable [ici](https://github.com/NepNath/TP-reseau/tree/main/TP%204/External%20files)


### 🌞 Analyser la capture Wireshark

* parmi ces 4 trames, laquelle contient les informations proposées au client ?
    c'est la tramme "DHCP Offer" qui contient les informations proposées au client
    