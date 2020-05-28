# Documentation générale du projet 4

Ce document présente globalement ce que nous avons mis en place grace au logiciel open source *GNS3*. Nous y décrirons les périphériques employés ainsi que les protocoles utilisés.

## 1 Topologie

![Capture GNS3](topologie.png)

## 2 Plan d'adressage
Le plan d'adressage de notre topologie est accessible ici *https://github.com/reseau-2020/projet-four/blob/master/topo/plan_adressage.md*.

### IPv4
En IPv4, nous avons utilisé des adresses en `10.32.X.X` pour les liaisons interne à la couche *CORE* et en `10.16.X.X` pour les liaisons entre les liaisons impliquant les couches *DISTRIBUTION* et *ACCESS*. Chaque sous-réseau possède un masque égal à 255.255.255.0. Le troisième octet des adresses renseigne sur la liaison entre les périphériques concernés. Par exemple, les routeurs *R1* et *R2* sont reliés en `10.32.12.1` (sur R1) et `10.32.12.2` (sur R2). On assigne 4 à *DS1* et 5 à *DS2*, ainsi *R3* et *DS2* sont reliés par `10.16.135.1` et `10.16.235.2` (sur *R3*), `10.16.135.2` et `10.16.235.1` (sur *DS2*).
Les *VLANs 10, 20, 30 et 40* prennent les adresses `10.32.10.X`, `10.32.20.X`, `10.32.30.X` et `10.32.40.X`.
Pour le site distant nous avons utilisé des adresses privées en `192.168.150.X`.

### Ipv6
L'adressage IPv6

## 3 VLAN

## 4 Spanning-tree
Le protocol *Spanning-tree* est implémenté sur les 4 périphériques de couche 2 : *AS1*, *AS2*, *DS1* & *DS2*. *DS1* est `root primary` pour les vlans 10, 30 et 99 (natif) et `secondary` pour les vlans 20 et 40. Respectivement, *DS2* est `root primary` pour les vlans 20 et 40 et `secondary` pour les vlans 10, 30 et 99.

## 5 Etherchannel
Nous avons monté 5 ports Etherchannel :

Ports channel | Ports physique | Commutateurs
|-------------|----------------|-------------
po1  | g0/0, g1/0 | AS1-DS1
po2  | g0/1, g1/1 | AS1-DS2
po3  | g0/2, g1/2 | DS1-DS2
po4  | g0/0, g1/0 | AS2-DS2
po5  | g0/1, g1/1 | AS2-DS1

## 6 HSRP
Le HSRP permet d'obtenir une continuité de service LAN sur les routeurs et assurer une diponibilité de passerelle d'un réseau en cas de problème. 
Sur DS1 HSRP est active pour VLAN10 et VLAN30.
sur DS2 HSRP est active pour VLAN20 et VLAN40.
L'adresse IP virtuelle associée au groupe est la passerelle du vlan. 
HSRP est implémenté en IPv4 et IPv6

## 7 DHCP & DNS
Les services *DHCP* et *DNS* sont déployés sur *DS1* et *DS2*, en IPv4 et IPv6.

Une verification pour le déploiement du *DNS* est d'essayer de joindre www.test.tf à partir d'un poste de travail 
````
[root@pc1 ~]# ping www.test.tf
PING test.tf (51.68.114.75) 56(84) bytes of data.
64 bytes from ip-51-68-114.eu (51.68.114.75): icmp_seq=1 ttl=48 time=12.6 ms
64 bytes from ip-51-68-114.eu (51.68.114.75): icmp_seq=2 ttl=48 time=12.4 ms
64 bytes from ip-51-68-114.eu (51.68.114.75): icmp_seq=3 ttl=48 time=12.9 ms
64 bytes from ip-51-68-114.eu (51.68.114.75): icmp_seq=4 ttl=48 time=12.1 ms
64 bytes from ip-51-68-114.eu (51.68.114.75): icmp_seq=5 ttl=48 time=12.8 ms

--- test.tf ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 6231ms
rtt min/avg/max/mdev = 12.166/12.619/12.997/0.320 ms
````

## 8 Protocole de routage EIGRP

Pour le routage entre la couche Distribution et la couche Core nous avons choisi d'utiliser le protocole de routage dynamique EIGRP notamment pour sa facilité de déploiement (vs OSPF) en IPv6.
EIGRP était un IGP propriétaire CISCO mais depuis 2013 il est devenu un standard de l'IETF partiellement ouvert.
Il utilise un protocole à vecteur de distances IP avec une distance administrative en interne de 90.

### 1. Configuration

Le routage EIGRP est activé sur les périphériques de couche 3 (R1, R2, R3, DS1 et DS2) sur le système autonome AS 1.
Un router-ID est associé à chaque routeur (1.1.1.1, 2.2.2.2,...) pour les différencier. Les interfaces qui ne participent pas au routage dynamique en local (interfaces VLAN ou vers internet) seront ajoutés
en passive-interface. Tous les réseaux adjacent au périphérique sont ajoutés au système autonome. On ajoute la commande `no auto-summary` pour ne pas agréger les routes dans la table de routage.
La route par défaut (vers internet) est distribuée par R1 en activant la commande `Redistribute static`

__Exemple sur R2:__

    
    router eigrp 1              ! --> Activation de routage en ipv4
     passive-interface g0/0
     eigrp router-id 2.2.2.2
     no auto-summary
     network 10.32.202.0        ! --> Ajout réseaux adjacents
     network 10.32.12.0
     ...
     
### 2. Vérification

Pour déboguer les erreurs EIGRP on peut utiliser les commandes suivantes :

* `show ip protocols`          --> Vérifier si le protocol est bien activer, voir network/passive interface
* `show ip eigrp neighbors`    --> Voir le voisinage du routeur en EIGRP avec Uptime/hold
* `show ip eigrp topology`     --> Voir la topology du réseau avec interfaces et adresses IP des autres routeurs
* `show ip route`              --> Voir toute la table de routage, les routes dynamique EIGRP sont symbolisés par la lettre D

## 9 NAT
Nous avons choisi la méthode de traduction dynamique overload (PAT) avec une seule IP globale sur *R1*. 
Après la défintion des adresses locales soumise au NAT, nous avons déployé la régle NAT sur l'interface connecté au nuage G0/1 qui est l'*outside interface*. Les autres interfaces sont définies comme *inside interface*

## 10 IPv6
## 11 Pare-feux & VPN IPsec
### Pare-feux
Nous avons mis en place deux pare-feux : un ZBF de Cisco sur *R1* dans le site principal et un pare-feu fortigate dans le site distant.
Sur le Cisco nous avons créé trois zone :
- Internet : `zone security lan`
- Lan : `zone security internet`
- DMZ : `zone security dmz`

Succinctement, les protocoles autorisés entre zones sont : 
- lan -> internet :  http, https, dns, icmp, ssh
- lan -> dmz : http, https, ssh, icmp
- internet -> dmz : http, https
- dmz -> internet :  http, https, dns, icmp, ssh

Nouss n'avons pas créé de zones dmz sur le site distant, ce dernier nous étant utile seulement pour construire un tunnel VPN.
 
### VPN
Nous avons monté un tunnel entre les deux sites via une authentification `esp-des` et un encryptage `esp-md5-hmac`. La différence des pare-feux de chaque côtés ainsi que les versions limitées offertes par *GNS3* ne nous ont pas permis d'avoir un tunnel 100% efficace. Il se monte bien dans le sens **Site Principal** => **Site Distant**, mais pas inversement.

## 12 Monitoring 
### SNMP
Le protocole SNMP permet la supervision et le diagnositque des problèmes. Dans notre topologie nous nous avons configuré le SNMPv2c de manière à ce que la communauté private soit activée en mode Read Only (RO), nous avons activé toutes les traps snmp qui seront envoyées et stokées sur le serveur *serveur-log*.

### SYSLOG
Nous avons configuré dans un premier lieu la machine centos *server-log* comme serveur syslog. Ensuite, nous avons configuré les client syslog sur les postes de travail et sur tout les éléments CISCO.

### NTP
Dans le but de sybchroniser l'horloge locale de notre réseau informatique, nous avons implémenté le NTP et nous avons choisi comme référence le serveur *pool.ntp.org*.

## 15 Sécurité 
### Radius

# Gestion des accès aux routeurs via un serveur Radius
### Création du serveur freeRadius sur un terminal Ubuntu

On a choisit de rajouter un pc ubuntu sur le switch relié a R3 pour gérer les authentification sur les périphériques de la couche core. 

    ! Installation du paquet freeradius
    apt-get update
    apt-get install freeradius
    ! Vérifie la version
    freeradius -v

    ! Chemin d'accès au fichiers de configuration
    cd /etc/freeradius/3.0

On ajoute les différents clients pour lesquels on utilisera l'authentification avec freeRadius dans un premier fichier. On ajoute un mot de passe qui servira à l'authentification entre les routeurs et le serveur Radius.

    vi clients.conf
    client 10.32.203.1 {
    secret = password
    nastype = cisco
    shortname = R3
    }

On ajoute ensuite les utilisateurs enregistrés sur les clients ainsi que leur mot de passe dans un deuxième fichier. On fixe le niveau de privilège (15=max). On a choisit d'ajouter un admin (lvl 15) et un utilisateur de base (lvl 1).

    vi users
    root Cleartext-Password := "testtest"
     Service-Type = NAS-Prompt-User,
     Cisco-AVPair = "shell:priv-lvl=15"
     
    user Cleartext-Password := "123"
     Service-Type = NAS-Prompt-User,
     Cisco-AVPair = "shell:priv-lvl=1"
     
**Important**, on doit redémarrer le service Freeradius pour prendre en compte les changements.

     service freeradius start
     service freeradius reload

### Configuration des routeurs R1 R2 R3 comme clients Radius
    
     privilege exec all level 5 show running-config
     file privilege 5
     privilege configure all level 5 logging
   
     aaa new-model           ! --> Activation de aaa
    
    radius server Radius-server                             ! --> Ajout d'un serveur radius avec son IPv4 et ports d'authentification
     address ipv4 10.32.203.3 auth-port 1812 acct-port 1813
     key password
    
    aaa authentication login AuthList1 local group radius none      ! --> Authentification AAA associé au serveur Radius
    aaa authorization exec AuthList1 local group radius none        ! --> Authorisation AAA associé au serveur Radius
    
    ip radius source-interface G0/3                                 ! --> Ajoute l'interface de connexion vers le serveur Radius
    radius-server attribute 6 on-for-login-auth
    
    aaa authorization console                              ! --> Configure les lines pour l'utilisation de AAA avec server radius
    line vty 0 4
    login authentication AuthList1
    authorization exec AuthList1
    line con 0
    login authentication AuthList1
    authorization exec AuthList1
    
### Diagnostics

    show run | in radius
    aaa authentication login default group radius local
    radius server Radius-server

    show run | in aaa
    aaa new-model
    aaa authentication login default group radius local
    aaa session-id common
    snmp-server enable traps aaa_server

### Switchport port Security
Nous avons activé la fonction de sécurité des ports de communtation afin de limiter les adresses autorisées à envoyer du trafic sur des ports de commutation individuels. Ceci est activé sur ports access de AS1 et AS2. 

## 17 Fiabilité de la topo 
### Vérification de la connectivité en IPV4 et IPV6
Des tests de connectivité en ipv4 et en ipv6 ont été établis en interne, vers l'internet et vers le site distant fortigate via le tunnel VPN. En outre, une connexion ssh est montée uniquement à partir de site cisco au site fortigate (via le tunnel VPN. 
 https://github.com/reseau-2020/projet-four/blob/master/topo/tests/connectivite_ipv4.md
 https://github.com/reseau-2020/projet-four/blob/master/topo/tests/connectivite_ipv6.md
### Vérification de la redondance STP
L'objectif de vérification du protocole Rapid Spanning-Tree est de prouver ses capacités de répartition de la charge des VLANs sur des liaisons Trunk alternatives tout en assurant sa mission de reprise suite à une rupture d'une liaison entre un commutateur de couche "Access" et un commutateur de couche "Distribution". Par exemple, dans le cadre de ce projet, grâce à Spanning-Tree, en cas de rupture de la liaison Po1 de la topologie, le trafic de VLANs 10 sera transféré via le commutateur "root secondary" alternatif qui est DS2 dans notre cas. 
 https://github.com/reseau-2020/projet-four/blob/master/topo/tests/Tests_fiabilit%C3%A9_STP.md
 ### Vérification de HSPR


