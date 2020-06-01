


 Pour répondre à l'aspect sécuritaire les technologies suivantes on été déployées:
 
 * SSH : Connexion distante avec le protocole de communication sécurisé SSH configurée sur tous les périphériques réseau
 * VLAN : les 4 VLANs déployées permettent de segmenter et d'isoler les flux des différents utilisateurs
 * Swithport security : option activée sur les switch de la couche Access, par défaut une seule adresse MAC est apprise dynamiquement, si elle change le port tombe en mode "shutdown"
 * BPDU guard : pour empêcher la modification de la topologie spanning tree (ajout d'un switch) la protection "BPDU guard" est activée sur les interfaces de AS1 et AS2.  Ainsi les messages BPDU ne seront pas acheminés sur les ports des VLANs.
 * Parefeu et DMZ : le parefeu CISCO ZBF protège la topologie des tentatives d'intrusion externe. Seul la DMZ (serveurs) est accessible de l'extérieur via une redirection de port.
 * Serveur FreeRADIUS : service de sécurité réseau AAA avec Authentification centralisée sur un serveur. Le serveur contient les noms d'utilisateurs, leurs mot de passes et leurs niveaux d'accès.
 * VPN IPsec : la communication avec le site distant est sécurisée par un tunnel VPN crypté en IPsec
 
 Le temps impartie au projet étant limité l'accent a été mis d'avantage sur la fiabilité de la solution que sur le focus sécuritaire.
 Pour aller plus loin dans la sécurisation du réseau il faudrait réaliser un audit de sécurité de la topologie existante et réfléchir à l'ajout d'autres technologies (exemples: DHCP Snooping, inspection couche 2, sécurité IPv6,..)
 
## Configuration du protocole SSH

Nous avons activé le protocole SSH sur tous les périphériques réseaux de notre topologie pour permettre l'administration en ligne de commandes sécurisée.
Pour configurer SSH il faut d'abord créer un nom d'hote et un nom de domaine puis ensuite générer une clé RSA (modulus 2048 bits ici).
On peut ensuite activer la version 2 du protocole. En option on ajoutera un time-out de 90 secondes et nous laisserons 2 tentatives de connexion  et un enregistrement des connexions ssh.

On ajoute ensuite ce mode de transport SSH aux consoles virtuelles (line vty) du périphérique.
```
 crypto-key generate rsa modulus 2048

 ip ssh version 2
 ip ssh time-out 90
 ip ssh authentication-retries 2
 ip ssh logging events

 line vty 0 4
 transport input ssh
 login local
```

L'authentification de la connexion se fait avec les utilisateurs enregistrés en local. Les mots de passes en local sont encryptés pour ne pas apparaitre en clair dans la configuration.



