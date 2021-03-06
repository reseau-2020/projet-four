# Documentation générale du projet 4
# Sommaire
--------------------------------------------------------------
1. [Topologie](#1)
2. [Plan d'adressage](#2)
3. [Les VLANs](#3)
4. [Spanning-Tree](#4)
5. [Etherchannel](#5)
6. [HSRP](#6)
7. [DHCP & DNS](#7)
8. [Protocole de routage : EIGRP](#8)
9. [Le NAT](#9)
10. [Pare-feux & VPN IPsec](#10)
11. [Monitoring](#11)
12. [Sécurité](#12)
13. [Fiabilité](#13)
14. [Sauvegarde des configurations avec Ansible](#14)
15. [Server Web sur site distant](#15)

--------------------------------------------------------


Ce document présente globalement ce que nous avons mis en place grace au logiciel open source *GNS3*. Nous y décrirons les périphériques employés ainsi que les protocoles utilisés.

# 1 Topologie <a id="1"></a>

![Capture GNS3](topologie.png)

## Inventaire ressources requises

Ci dessous un tableau avec les ressources matérielles utilisées. 

   |Couche | Ressources | 
   |-------|----|
   |Couche access| <ul><li>Deux switchs AS1 et AS2 Cisco IOS Software, vios_l2 Software (vios_l2-ADVENTERPRISEK9-M) Experimental Version 15.2(20170321:233949)</li><li> 8 postes de travail CentOS Linux release 7.5.1804 (Core)</li></ul> |
   |Couche distribution| <ul><li> Deux switchs de distribution DS1 et DS2 Cisco IOS Software, vios_l2 Software (vios_l2-ADVENTERPRISEK9-M), Experimental Version 15.2(20170321:233949) </li></ul> |
   |Couche core|<ul><li>Trois routeurs R1, R2 et R3 Cisco IOS Software, IOSv Software (VIOS-ADVENTERPRISEK9-M),  Version 15.6(2)T, RELEASE SOFTWARE (fc2) </li><li> Trois switchs Cisco IOS Software, vios_l2 Software (vCCios_l2-ADVENTERPRISEK9-M), Experimental Version 15.2(20170321:233949) </li><li> Deux CentOS Linux release 8.1.1911 (Core) </li><li> Un Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-62-generic x86_64)</li></ul> |
   |Site fortigate | <ul><li> Pare-feu fortinet : Model name: FortiGate-VM64-KVM, CPU: QEMU Virtual CPU version 2.5+ </li><li> Deux switchs : Cisco IOS Software, vios_l2 Software (vios_l2-ADVENTERPRISEK9-M), Experimental Version 15.2(20170321:233949) </li><li> Deux ordinateurs Centos : CentOS Linux release 7.6.1810 (Core) </li><li> Un serveur Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-62-generic x86_64) </li></ul> |
   |Site contôleur | <ul><li> Un switch Cisco IOS Software, vios_l2 Software (vios_l2-ADVENTERPRISEK9-M), Experimental Version 15.2(20170321:233949) </li><li> Un CentOS Linux release 7.6.1810 (Core) </li></ul> |
    


# 2 Plan d'adressage <a id="2"></a>
Le plan d'adressage de notre topologie est accessible ici *https://github.com/reseau-2020/projet-four/blob/master/topo/plan_adressage.md*.

## IPv4
En IPv4, nous avons utilisé des adresses en `10.32.X.X` pour les liaisons interne à la couche *CORE* et en `10.16.X.X` pour les liaisons entre les liaisons impliquant les couches *DISTRIBUTION* et *ACCESS*. Chaque sous-réseau possède un masque égal à 255.255.255.0. Le troisième octet des adresses renseigne sur la liaison entre les périphériques concernés. Par exemple, les routeurs *R1* et *R2* sont reliés en `10.32.12.1` (sur R1) et `10.32.12.2` (sur R2). On assigne 4 à *DS1* et 5 à *DS2*, ainsi *R3* et *DS2* sont reliés par `10.16.135.1` et `10.16.235.2` (sur *R3*), `10.16.135.2` et `10.16.235.1` (sur *DS2*).
Les *VLANs 10, 20, 30 et 40* prennent les adresses `10.16.10.X`, `10.16.20.X`, `10.16.30.X` et `10.16.40.X`.
Pour le site distant nous avons utilisé des adresses privées en `192.168.150.X`.

## Ipv6
Concernant l'adressage IPv6 (/64 par défaut), les adresses link-local sont :
- sur R1 : `fe80::1` (`fe80::cafe:4` sur g0/1 qui connecte l'internet)
- sur R2 : `fe80::2`
- sur R3 : `fe80::3`
- sur DS1 : `fe80::d:1`
- sur DS2 : `fe80::d:2`
- sur DS1 VLAN 10 : `fe80::d1:10`
- sur DS1 VLAN 20 : `fe80::d1:20`
- sur DS1 VLAN 30 : `fe80::d1:30`
- sur DS1 VLAN 40 : `fe80::d1:40`
- sur DS2 VLAN 10 : `fe80::d2:10`
- sur DS2 VLAN 20 : `fe80::d2:20`
- sur DS2 VLAN 30 : `fe80::d2:30`
- sur DS2 VLAN 40 : `fe80::d2:40`

les adresses privées sont :
- sur R1 (g0/0) : `2001:470:c814:4001::1:1`
- sur R2 (g0/0) : `2001:470:c814:4002::2:1`
- sur R3 (g0/0) : `2001:470:c814:4003::3:1`
- sur DS1 VLAN 10 : `2001:470:c814:4011::`
- sur DS1 VLAN 20 : `2001:470:c814:4021::`
- sur DS1 VLAN 30 : `2001:470:c814:4031::`
- sur DS1 VLAN 40 : `2001:470:c814:4041::`
- sur DS2 VLAN 10 : `2001:470:c814:4012::`
- sur DS2 VLAN 20 : `2001:470:c814:4022::`
- sur DS2 VLAN 30 : `2001:470:c814:4032::`
- sur DS2 VLAN 40 : `2001:470:c814:4042::`

et les adresses publiques sont :
- sur R1 (g0/0) : `fd00:fd00:fd00:1::1:1`
- sur R2 (g0/0) : `fd00:fd00:fd00:2::2:1`
- sur R3 (g0/0) : `fd00:fd00:fd00:3::3:1`
- sur DS1 VLAN 10 : `fd00:1ab:10::1`
- sur DS1 VLAN 20 : `fd00:1ab:20::1`
- sur DS1 VLAN 30 : `fd00:1ab:30::1`
- sur DS1 VLAN 40 : `fd00:1ab:40::1`
- sur DS2 VLAN 10 : `fd00:1ab:10::2`
- sur DS2 VLAN 20 : `fd00:1ab:20::2`
- sur DS2 VLAN 30 : `fd00:1ab:30::2`
- sur DS2 VLAN 40 : `fd00:1ab:40::2`

Nous n'avons pas attribué d'adresses IPv6 dans le site distant par manque de temps pour tester le tunnel VPN en IPv6. *DS1* et *DS2* jouent le rôle de serveur DHCPv6.

# 3 Les VLANs <a id="3"></a>

Pour segmenter logiquement le réseau de la couche Access nous avons crée 4 VLANs pour 4 types d'utilisateurs différents :

* VLAN 10 : DATA
* VLAN 20 : VOICE
* VLAN 30 : CAMERA
* VLAN 40 : EXECUTIVE

La configuration des VLANs permet de résoudre plusieurs problèmes :

1. La sécurité : les VLANs permettent d'isoler les flux de données en fonction des utilisateurs (interfaces) mais aussi d'isoler certaines parties du réseau (server) sans recours à un routeur.
2. L'optimisation : avec une segmentation logique on peut créer plusieurs réseaux sans avoir besoin d'ajouter des switchs et des câbles
3. La qualité de service : On peut réserver de la bande passante pour certains usages (VoIP)

## 3.1 Configuration

On commence par créer et nommer les différents VLANs sur les périphériques des couches Access et Distribution (DS1&2, AS1&2):

    vlan 10
    name DATA
    ...

Les interfaces physiques sur lesquelles le trafic de plusieurs vlans doit passer seront montées en mode trunk en ajoutant le protocole d'encapsulation dot1q (IEEE 802.1q).
Ce standard permet de modifier les trames Ethernet pour fournir un mécanisme d'encapsulation qui permet de faire passer le traffic de plusieurs VLANs sur un seul lien physique.
Le VLAN 99 sera le Vlan Natif, il sera utilisé pour le transport des trames ethernet non taggés sur les interfaces en mode trunk.

Le trunking est activé sur les interfaces de liaison entre la couche Access et Distribution (AS --> DS) mais aussi sur les interfaces de liaisons entre DS1 et DS2 qui assurent une redondance de liens.

    interface range g0/0,g1/0
     shutdown
     switchport trunk encapsulation dot1q     ! --> On active le protocole dot1q
     switchport trunk native vlan 99          ! --> On renseigne le VLAN natif
     switchport mode trunk                    ! --> On force le passage du mode DTP à "ON" pour activer le trunking
     no shutdown

## 3.2 Adressage des Vlans

On configure ensuite les interfaces virtuelles VLAN que l'on a créee sur différentes plages d'adresses IPv4 et IPv6.
Dans notre topologie on a choisit de faire varier le troisième octet du bloque d'adresses IPv4 pour différentier logiquement les périphériques des différents VLANs.

   |VLAN | Adresses ipv4  |  Adresses ipv6
   |-----|----|----|
   | VLAN10 | `10.16.10.0/24` | `fe80::d1:10` ; `fd00:1ab:10::1` ; `2001:470:c814:4011::`
   | VLAN20 | `10.16.20.0/24` | `fe80::d1:20` ; `fd00:1ab:20::1` ; `2001:470:c814:4021::` 
   | VLAN30 | `10.16.30.0/24` | `fe80::d1:30` ; `fd00:1ab:30::1` ; `2001:470:c814:4031::`
   | VLAN40 | `10.16.40.0/24` | `fe80::d1:40` ; `fd00:1ab:40::1` ; `2001:470:c814:4041::`
   
On configure les interfaces VLANs sur les périphériques DS1 et DS2. Sur le dernier octet on choisit d'attibuer 252 sur les interfaces de DS1 et 253 pour celles de DS2.

__Exemple vlan10 sur DS1:__

    interface vlan 10
     ip address 10.16.10.252 255.255.255.0
     ipv6 address fe80::d1:10 link-local
     ipv6 address fd00:1ab:10::1/64
     ipv6 address 2001:470:c814:4011::/64
     no shutdown
     ...
 
 Pour la mise en place du protocole de redondance de premier lien avec HSRP on utilisera les adresses virtuelles terminant en .254 (_ex: 10.16.10.254_) on utilisera aussi ces adresses comme passerelles lors de la configuration du DHCPv4.
 (Voir chapitres HSRP et DHCP).
 
 ## 3.3 Diagnostique

Pour diagnostiquer des erreurs sur les VLANs on peut utiliser les commandes suivantes:

- `show vlan`                   --> Voir les VLANs et les interfaces physiques associées
- `show interface trunk`        --> Voir les interfaces configurées en trunk
- `show dtp`                    --> Voir les paramètres du Dynamique Trunk Protocol
- `show interface switchport`   --> Voir la configuration de toutes les interfaces switchport 

# 4 Spanning-tree <a id="4"></a>
Le protocol *Spanning-tree* est implémenté sur les 4 périphériques de couche 2 : *AS1*, *AS2*, *DS1* & *DS2*. *DS1* est `root primary` pour les vlans 10, 30 et 99 (natif) et `secondary` pour les vlans 20 et 40. Respectivement, *DS2* est `root primary` pour les vlans 20 et 40 et `secondary` pour les vlans 10, 30 et 99. Pour vérifier l'implémentation du SPT, on a éxécuté les commandes suivantes:
- show spanning-tree summary
````
DS1#show spanning-tree summary
Switch is in rapid-pvst mode
Root bridge for: VLAN0010, VLAN0030, VLAN0099
Extended system ID                      is enabled
Portfast Default                        is disabled
Portfast Edge BPDU Guard Default        is disabled
Portfast Edge BPDU Filter Default       is disabled
Loopguard Default                       is disabled
PVST Simulation Default                 is enabled but inactive in rapid-pvst mode
Bridge Assurance                        is enabled
EtherChannel misconfig guard            is enabled
Configured Pathcost method used is short
UplinkFast                              is disabled
BackboneFast                            is disabled

Name                   Blocking Listening Learning Forwarding STP Active
---------------------- -------- --------- -------- ---------- ----------
VLAN0001                     0         0        2          1          3
VLAN0010                     0         0        0          3          3
VLAN0020                     0         0        0          3          3
VLAN0030                     0         0        0          3          3
VLAN0040                     0         0        0          3          3

Name                   Blocking Listening Learning Forwarding STP Active
---------------------- -------- --------- -------- ---------- ----------
VLAN0099                     0         0        0          3          3
---------------------- -------- --------- -------- ---------- ----------
6 vlans                      0         0        2         16         18
````

- show spanning-tree vlan X 
````
DS1#show spanning-tree vlan 20

VLAN0020
  Spanning tree enabled protocol rstp
  Root ID    Priority    24596
             Address     0c8c.1297.0100
             Cost        3
             Port        66 (Port-channel3)
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    28692  (priority 28672 sys-id-ext 20)
             Address     0c8c.127d.9c00
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  300 sec

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Po1                 Desg FWD 3         128.65   P2p Peer(STP)
Po3                 Root FWD 3         128.66   P2p
Po5                 Desg FWD 3         128.67   P2p Peer(STP)
````

# 5 Etherchannel <a id="5"></a>

Pour la communication entre la couche Access et la couche Distribution appelé "switch block" nous avons utilisé la technologie Etherchannel (ou Portchannel) propriétaire cisco 
qui existe aussi en version ouverte avec le standard IEEE 802.3ad
Etherchannel permet d'assembler plusieurs liens physiques en un seul lien logique (agrégation de liens) dans le but d'augmenter la vitesse mais aussi la tolérance aux pannes.
Cela permettra d'augmenter la bande passante dans le "switch block".

## 5.1 Configuration

Dans notre topologie nous avons configuré 5 ports Etherchannel :

Ports channel | Ports physique | Commutateurs
|-------------|----------------|-------------
po1  | g0/0, g1/0 | AS1-DS1
po2  | g0/1, g1/1 | AS1-DS2
po3  | g0/2, g1/2 | DS1-DS2
po4  | g0/0, g1/0 | AS2-DS2
po5  | g0/1, g1/1 | AS2-DS1

Le maillage entre liaisons Etherchannels entre les switch Access (AS1&2) et les switch distribution (DS1&2) permettent d'assurer une redondance de liens.
Pour configurer un lien Etherchannel on assigne 2 interfaces au même channel-group et on active le mode `desirable` pour avoir une configuration dynamique d'Etherchannel avec le périphérique relié au même lien physique.

__Exemple configuration sur DS1:__

    interface range g0/0,g1/0
     shutdown
     channel-group 1 mode desirable   ! --> Chaque lien etherchannel correspond a un numéro de groupe différent
     no shutdown
     ...
   
Le trunking doit aussi être activé sur les liens Etherchannels.

## 5.2 Diagnostiques

Les commandes suivantes permettent de diagnostiquer des erreurs sur Etherchannel:

- `show interface etherchannel`                                                --> Voir les interfaces configurées en Etherchannel
- `show etherchannel [summary | port | load-balance | port-channel | detail]`  --> Voir le détailde la configuration Etherchannel
- `show [pagp | lacp ] neighbors`                                              --> En config dynamique voir le voisinage Etherchannel

# 6 HSRP <a id="6"></a>
Le HSRP permet d'obtenir une continuité de service LAN sur les routeurs et assurer une diponibilité de passerelle d'un réseau en cas de problème. 
Sur DS1 HSRP est active pour VLAN10 et VLAN30.
sur DS2 HSRP est active pour VLAN20 et VLAN40.
L'adresse IP virtuelle associée au groupe est la passerelle du vlan. 
HSRP est implémenté en IPv4 et IPv6 (les root secondary et primary dans notre cas sont inversés sur DS1 et DS2)
````
DS1#show standby brief
                     P indicates configured to preempt.
                     |
Interface   Grp  Pri P State   Active          Standby         Virtual IP
Vl10        10   150 P Active  local           10.16.10.253    10.16.10.254
Vl10        16   150   Standby FE80::D2:10     local           FE80::D10
Vl20        20   100   Standby 10.16.20.253    local           10.16.20.254
Vl20        26   100   Standby FE80::D2:20     local           FE80::D20
Vl30        30   150 P Active  local           10.16.30.253    10.16.30.254
Vl30        36   150   Standby FE80::D2:30     local           FE80::D30
Vl40        40   100   Standby 10.16.40.253    local           10.16.40.254
Vl40        46   100   Standby FE80::D2:40     local           FE80::D40
````

Pour la vérification de l'implémentation du protocole HSPR, on a utilisé les commandes suivantes:
- show standby
- show standby neighbors
- show standby brief

# 7 DHCP & DNS <a id="7"></a>

## 7.1 Configuration du DHCP

Les adresses IPv4 et IPv6 des terminaux de la couche Access sont distribués automatiquement par DHCP.
DS1 et DS2 font office de server DHCP sur notre topologie. 

Au total 4 pools DHCP, une pour chaque VLAN, sont paramétrés sur chacun des périphériques de la couche Distribution.
En plus des adresses IP, le server DHCP pousse aussi l'adresse de la passerelle (IP virtuelle du HSRP) et l'adresse du DNS.
La durée du bail DHCP est fixée à 8 heures

__Exemple pour le VLAN 20 sur DS1:__

    ip dhcp pool VLAN20
      network 10.16.20.0 255.255.255.0
      default-router 10.16.20.254
      dns-server 1.1.1.1
      lease 0 8

Nous avons choisi de ne pas utiliser de DHCP Relay, à la place les 2 servers DHCP utilisent des plages d'adresses
complémentaires qui ne se chevauchent pas.

__Exclusion de plages d'adresses sur VLAN 20 de DS1:__

`ip dhcp excluded-address 10.16.20.128 10.16.20.255`

Quatres autres pools DHCP sont configurés sur DS1 et DS2 pour servir les adresses IPv6 publiques en utilisant un prefixe. Le serveur DNS IPv6 est aussi poussé par le server.

    ipv6 dhcp pool DHCPv6-VLAN30
     address prefix 2001:470:C814:4032::/64
     dns-server 2606:4700:4700::1111
     domain-name projet4.com
     
## 7.3 Configuration du DNS

Comme server DNS nous utilisons le server publique `1.1.1.1` car il est réputé plus confidentiel pour les données. 
Il est configuré sur chaque périphérique réseaux avec la commande:

     ip name-server 1.1.1.1

## 7.4 Vérifications

On peut vérifier le bon fonctionnement du DHCP en scanant le trafic entre PC1 et AS1 et en envoyant un premier ping.
On observe bien les 4 étapes (DORA) du processus d'obtention d'une adresse en DHCP:

![DORA](DORA.png)

Une verification pour le déploiement du *DNS* est d'essayer de joindre www.test.tf à partir d'un poste de travail 
````
[root@pc1 ~]# ping www.test.tf
PING test.tf (51.68.114.75) 56(84) bytes of data.
64 bytes from ip-51-68-114.eu (51.68.114.75): icmp_seq=1 ttl=48 time=12.6 ms
64 bytes from ip-51-68-114.eu (51.68.114.75): icmp_seq=2 ttl=48 time=12.4 ms
...
--- test.tf ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 6231ms
rtt min/avg/max/mdev = 12.166/12.619/12.997/0.320 ms
````

et en IPv6
````
[root@pc8 ~]# ping6 test.tf
PING test.tf(2001:41d0:305:1000::1d8a (2001:41d0:305:1000::1d8a)) 56 data bytes
64 bytes from 2001:41d0:305:1000::1d8a (2001:41d0:305:1000::1d8a): icmp_seq=1 ttl=49 time=18.8 ms
64 bytes from 2001:41d0:305:1000::1d8a (2001:41d0:305:1000::1d8a): icmp_seq=2 ttl=49 time=14.6 ms
...
--- test.tf ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 14.380/15.698/18.810/1.815 ms
````

# 8 Protocole de routage EIGRP <a id="8"></a>

Pour le routage entre la couche Distribution et la couche Core nous avons choisi d'utiliser le protocole de routage dynamique EIGRP notamment pour sa facilité de déploiement (vs OSPF) en IPv6.
EIGRP était un IGP propriétaire CISCO mais depuis 2013 il est devenu un standard de l'IETF partiellement ouvert.
Il utilise un protocole à vecteur de distances IP avec une distance administrative en interne de 90.

## 8.1 Configuration

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
     
## 8.2 Vérification

Pour déboguer les erreurs EIGRP on peut utiliser les commandes suivantes :

* `show ip protocols`          --> Vérifier si le protocol est bien activer, voir network/passive interface
* `show ip eigrp neighbors`    --> Voir le voisinage du routeur en EIGRP avec Uptime/hold
* `show ip eigrp topology`     --> Voir la topology du réseau avec interfaces et adresses IP des autres routeurs
* `show ip route`              --> Voir toute la table de routage, les routes dynamique EIGRP sont symbolisés par la lettre D

# 9 NAT <a id="9"></a>
Nous avons choisi la méthode de traduction dynamique overload (PAT) avec une seule IP globale sur *R1*. 
Après la défintion des adresses locales soumise au NAT, nous avons déployé la régle NAT sur l'interface connecté au nuage G0/1 qui est l'*outside interface*. Les autres interfaces sont définies comme *inside interface*

Le *show ip statistivs* nous donne une aperçu sur les traductions nat actives et la régle nat.
````
R1#show ip nat statistics
Total active translations: 24 (0 static, 24 dynamic; 24 extended)
Peak translations: 318, occurred 00:38:17 ago
Outside interfaces:
  GigabitEthernet0/1
Inside interfaces:
  GigabitEthernet0/0, GigabitEthernet0/2, GigabitEthernet0/3
Hits: 882  Misses: 0
CEF Translated packets: 573, CEF Punted packets: 309
Expired translations: 612
Dynamic mappings:
-- Inside Source
[Id: 1] access-list lan interface GigabitEthernet0/1 refcount 22

Total doors: 0
Appl doors: 0
Normal doors: 0
Queued Packets: 0
````

# 10 Pare-feux & VPN IPsec <a id="10"></a>
## 10.1 Pare-feux
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
 
## 10.2 VPN IPsec site-à-site

Pour sécuriser la connexion entre les 2 sites distants nous avons configuré un tunnel VPN IPsec. 
Le tunnel VPN permet de créer un lien direct entre des réseaux distants et d'isoler leurs échanges du reste du trafic sur le réseau publique.
Le protocole IPsec permet lui d'authentifier et de chiffrer les données, ainsi le flux n'est compréhensible que par le destinataire et ne peut être modifié.
C'est ce protocole qui apporte l'aspect sécurité du tunnel.

Pour être fonctionnel le tunnel doit être configuré sur les 2 sites distants, nous l'avons donc déployé sur le pare-feu Fortigate et également sur le routeur CISCO R1.

## 10.3 Configuration sur Fortigate

Côté fortigate on utilise l'interface web du pare-feu en se connectant via l'adresse IP d'une des interfaces. 
Dans le menu `VPN --> IPsec Wizard` on peut déployer un tunnet "par défault" en suivant les 3 étapes de l'assistant:

1. VPN Setup :
    - Nom : 'Branch-to-HQ'
    - Template Type : Site-to-Site
    - Remote device Type : CISCO
    - NAT Configuration : No NAT between sites
    
2. Authentification :
    - Remote Device : IP Address
    - IP Address : 192.168.122.18
    - Outgoing interface : port3
    - Authentication : Pre-shared key (********)
    
3. Policy&Routing:
    - Local Interface : port2
    - Local Subnet : 192.168.150.0/24
    - Remote Subnets : 10.0.0.0/8
    - Internet Access : None

Après avoir configuré le VPN IPsec par défaut nous devons personnaliser les paramètres d'authentification et de chiffrement.
Dans le menu `VPN --> IPsec Tunnels` nous devons éditer notre VPN et cliquer sur 'Custom VPN' pour modifier ces paramètres.

- Phase 1 :
    * Algorithms : DES-MD5
    * Diffie-Hellman Group : 5

- Phase 2 :
    * Algorithms : DES-MD5
    * Diffie-Hellman Group : None

Après avoir validé cette étape le pare-feu est monté du côté du site distant, il reste ensuite à le configurer sur le routeur Cisco.

## 10.4 Configuration du VPN sur le routeur R1

On commence par créer le groupe isakmp auquel on va attribuer les paramètres Internet Key Exchange (IKE). 
Ensuite on rajoute la clé d'authentification associé à l'adresse IP du Fortigate.
```
crypto isakmp policy 1
 encr des
 hash md5
 authentication pre-share
 group 5
 lifetime 7200
crypto isakmp key ******** address 192.168.122.27 
```
On crée un transform-set pour les paramètres IPsec (phase2) que l'on ajoute à la crypto-map.
 
```
crypto ipsec transform-set to-fortigate-set esp-des esp-md5-hmac.

crypto map cm-to-fortigate 1 ipsec-isakmp
 set peer 192.168.122.29
 set transform-set to-fortigate-set
 match address crypto-acl
```
Pour finir on ajoute la crypto map à l'interface connectée au WAN.
```
interface G0/1	
 crypto map cm-to-fortigate
```
Le tunnel est configuré mais le parefeu et les ACLs doivent encore être adaptés pour laisser passer le traffic venant du tunnel.
```
ip access-list extended ISAKMP_IPSEC
 permit udp any any eq isakmp
 permit ahp any any
 permit esp any any
 permit udp any any eq non500-isakmp
class-map type inspect match-any vpn-class
 match access-group name ISAKMP_IPSEC
policy-map type inspect to-self-policy
 class type inspect vpn-class
  inspect
```

La différence des pare-feux de chaque côtés ainsi que les versions limitées offertes par GNS3 ne nous ont pas permis d'avoir un tunnel 100% efficace.
Il se monte bien dans le sens Site Principal => Site Distant, mais pas inversement.


# 11 Monitoring <a id="11"></a>
## SNMP
Le protocole SNMP permet la supervision et le diagnositque des problèmes. Dans notre topologie nous avons configuré le SNMPv2c de manière à ce que la communauté private soit activée en mode Read Only (RO), nous avons activé toutes les traps snmp qui seront envoyées et stokées sur le serveur *serveur-log*.

__Exemple sur R1__

````
R1#show snmp
0 SNMP packets input
    0 Bad SNMP version errors
    0 Unknown community name
    0 Illegal operation for community name supplied
    0 Encoding errors
    0 Number of requested variables
    0 Number of altered variables
    0 Get-request PDUs
    0 Get-next PDUs
    0 Set-request PDUs
    0 Input queue packet drops (Maximum queue size 1000)
31 SNMP packets output
    0 Too big errors (Maximum packet size 1500)
    0 No such name errors
    0 Bad values errors
    0 General errors
    0 Response PDUs
    31 Trap PDUs
SNMP Dispatcher:
   queue 0/75 (current/max), 0 dropped
SNMP Engine:
   queue 0/1000 (current/max), 0 dropped

SNMP logging: enabled
    Logging to 10.32.202.3.162, 0/10, 30 sent, 1 dropped.
````
__SNMP traps collectés sur le serveur__
````
[root@pc1-r2 ~]# snmpwalk -v2c -cprivate 10.32.12.1
SNMPv2-MIB::sysDescr.0 = STRING: Cisco IOS Software, IOSv Software (VIOS-ADVENTERPRISEK9-M), Version 15.6(2)T, RELEASE SOFTWARE (fc2)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2016 by Cisco Systems, Inc.
Compiled Tue 22-Mar-16 16:19 by prod_rel_team
SNMPv2-MIB::sysObjectID.0 = OID: SNMPv2-SMI::enterprises.9.1.1041
DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (1101804) 3:03:38.04
SNMPv2-MIB::sysContact.0 = STRING:
SNMPv2-MIB::sysName.0 = STRING: R1.LAN.PROJECT4
SNMPv2-MIB::sysLocation.0 = STRING:
SNMPv2-MIB::sysServices.0 = INTEGER: 78
SNMPv2-MIB::sysORLastChange.0 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORID.1 = OID: SNMPv2-SMI::enterprises.9.7.129
SNMPv2-MIB::sysORID.2 = OID: SNMPv2-SMI::enterprises.9.7.115
SNMPv2-MIB::sysORID.3 = OID: SNMPv2-SMI::enterprises.9.7.265
SNMPv2-MIB::sysORID.4 = OID: SNMPv2-SMI::enterprises.9.7.112
SNMPv2-MIB::sysORID.5 = OID: SNMPv2-SMI::enterprises.9.7.106
SNMPv2-MIB::sysORID.6 = OID: SNMPv2-SMI::enterprises.9.7.47
SNMPv2-MIB::sysORID.7 = OID: SNMPv2-SMI::enterprises.9.7.122
SNMPv2-MIB::sysORID.8 = OID: SNMPv2-SMI::enterprises.9.7.37
SNMPv2-MIB::sysORID.9 = OID: SNMPv2-SMI::enterprises.9.7.92
SNMPv2-MIB::sysORID.10 = OID: SNMPv2-SMI::enterprises.9.7.53
SNMPv2-MIB::sysORID.11 = OID: SNMPv2-SMI::enterprises.9.7.54
SNMPv2-MIB::sysORID.12 = OID: SNMPv2-SMI::enterprises.9.7.52
SNMPv2-MIB::sysORID.13 = OID: SNMPv2-SMI::enterprises.9.7.93
SNMPv2-MIB::sysORID.14 = OID: SNMPv2-SMI::enterprises.9.7.186
````

## SYSLOG
Nous avons configuré dans un premier lieu la machine centos *server-log* comme serveur syslog. Ensuite, nous avons configuré les client syslog sur les postes de travail et sur tout les éléments CISCO. 

Ci dessous, les loggs aperçus sur le serveur syslog suite à une shutdown sur une interface d'un des routeurs de notre topologie. 

````
2020-05-28T10:04:03.567211+02:00 _gateway 57: R2: *May 28 08:04:00: %DUAL-5-NBRCHANGE: EIGRP-IPv6 1: Neighbor FE80::1 (GigabitEthernet0/1) is down: interface down
2020-05-28T10:04:03.568226+02:00 _gateway 58: R2: *May 28 08:04:00: %DUAL-5-NBRCHANGE: EIGRP-IPv4 1: Neighbor 10.32.12.1 (GigabitEthernet0/1) is down: interface down
2020-05-28T10:04:05.548297+02:00 _gateway 59: R2: *May 28 08:04:02: %LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to administratively down
2020-05-28T10:04:05.548945+02:00 _gateway 60: R2: *May 28 08:04:03: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to down
2020-05-28T10:04:09.751601+02:00 _gateway 61: R2: *May 28 08:04:07: %LINK-3-UPDOWN: Interface GigabitEthernet0/1, changed state to up
2020-05-28T10:04:09.755683+02:00 _gateway 62: R2: *May 28 08:04:08: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to up
2020-05-28T10:04:13.454673+02:00 _gateway 63: R2: *May 28 08:04:10: %DUAL-5-NBRCHANGE: EIGRP-IPv6 1: Neighbor FE80::1 (GigabitEthernet0/1) is up: new adjacency
2020-05-28T10:04:13.458910+02:00 _gateway 64: R2: *May 28 08:04:11: %DUAL-5-NBRCHANGE: EIGRP-IPv4 1: Neighbor 10.32.12.1 (GigabitEthernet0/1) is up: new adjacency

````
## NTP
Dans le but de sybchroniser l'horloge locale de notre réseau informatique, nous avons implémenté le NTP et nous avons choisi comme référence le serveur *3.fr.pool.ntp.org*.

# 12 Sécurité <a id="12"></a>

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

## Switchport Security

Le mode switchport security est simplement activé sur les interfaces des switchs AS1 et AS2 de la couche Access. Par défaut, il permet qu'une seule adresse MAC soit apprise dynamiquement, en cas de "violation" il passe en mode "shutdown".
```
interface g0/1
 switchport port security

show port-security
```
## BPDU guard
En activant le mode BPDU guard sur les port configurés en "PortFast" on empêche les flux de messages BPDUs d'être acheminés, ce qui empêche donc la modification de la topologie Spanning-tree:
```
interface g0/1
 spanning-tree portfast
 spanning-tree bpdu guard enable
```
Ou en global pour toutes les interfaces non trunk :
```
spanning-tree portfast default
spanning-tree portfast bpdu guard default
```
Grâce à ça, si un attaquant essaie de connecter un autre Switch utilisant le protocole Spanning-Tree il ne pourra pas devenir Root et influencer le protocole.

## Serveur Radius

Un service de sécurité AAA permet un contôle d'accès aux périphériques du réseaux.
Il réalise les 3 fonctions suivantes :

1. Authentification : contrôle qui est autorisé à accéder au réseau
2. Authorization : contrôle ce que les utilisateurs peuvent faire
3. Accounting : vérifie les actions qui ont été accomplies par les utilisateurs

Dans notre topologie nous avons utilisé le protocole RADIUS avec le logiciel opensource FreeRADIUS.

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

On ajoute ensuite les utilisateurs enregistrés sur les clients ainsi que leur mot de passe dans un deuxième fichier. On fixe le niveau de privilège (15=max). On a choisit d'ajouter un admin (lvl 15) et un utilisateur de base (lvl 5).

    vi users
    root Cleartext-Password := "testtest"
     Service-Type = NAS-Prompt-User,
     Cisco-AVPair = "shell:priv-lvl=15"
     
    user Cleartext-Password := "123"
     Service-Type = NAS-Prompt-User,
     Cisco-AVPair = "shell:priv-lvl=5"
     
**Important**, on doit redémarrer le service Freeradius pour prendre en compte les changements.

     service freeradius start
     service freeradius reload

### Configuration des routeurs R1 R2 R3 comme clients Radius
    
    ! On doit paramétrer les droits d'accès d'un utilisateur avec le niveau de privilège 5
     privilege exec all level 5 show running-config
     file privilege 5
     privilege configure all level 5 logging
   
     aaa new-model           ! --> Activation de AAA
    
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

En capturant le trafic avec Wireshark :

![Capture_Datagrammes](RADIUS.JPG)

# 13 Fiabilité de la topo <a id="13"></a>
## Vérification de la connectivité en IPV4 et IPV6
Des tests de connectivité en ipv4 et en ipv6 ont été établis en interne, vers l'internet et vers le site distant fortigate via le tunnel VPN. En outre, une connexion ssh est montée uniquement à partir de site cisco au site fortigate (via le tunnel VPN). 
 https://github.com/reseau-2020/projet-four/blob/master/topo/tests/Connectivit%C3%A9_ipv4.md
 https://github.com/reseau-2020/projet-four/blob/master/topo/tests/connectivite_ipv6.md
## Vérification de la redondance STP et de la technologie HSRP
L'objectif de vérification du protocole Rapid Spanning-Tree est de prouver ses capacités de répartition de la charge des VLANs sur des liaisons Trunk alternatives tout en assurant sa mission de reprise suite à une rupture d'une liaison entre un commutateur de couche "Access" et un commutateur de couche "Distribution". Par exemple, dans le cadre de ce projet, grâce à Spanning-Tree, en cas de rupture de la liaison Po1 de la topologie, le trafic de VLANs 10 sera transféré via le commutateur "root secondary" alternatif qui est DS2 dans notre cas. En outre, pour vérifier la fiabilité de HSRP, on a fait tomber la passerelle DS1 lors d'un ping en continu de pc1 vers le routeur R2: après quelques paquets perdus le traffic est enfin repris par DS2 et R2 est de nouveau joignable (root secondary).  
Test en IPv4: https://github.com/reseau-2020/projet-four/blob/master/topo/tests/Fiabilit%C3%A9_STP-HSRP_IPV4.md

Test en IPv6: https://github.com/reseau-2020/projet-four/blob/master/topo/tests/test%20STP%20IPv6.md

# 14 Sauvegarde des configurations des périphériques <a id="14"></a>
Nous utilisons Ansible depuis la station de contrôle reliée à tous les périphériques afin de sauvegarder les configs.

Les fichiers des périphériques présent dans le dossier `ansible-projet4/playbooks/inventories/ccna/host_vars/` ont été mis à jour avec les bonnes adresses sur les interfaces.

De plus la connexion aux switchs *AS1* et *DS1* ne s'effectuant pas (problème de privilège), nous avons rajouté `ansible_become_pass=testtest` au fichier `ansible-projet4/playbooks/inventories/ccna_projet4/hosts`. Cependant le problème persiste sur *DS1*.

Le livre de jeux `backup.yml` présent dans `ansible-projet4/playbooks/` sauvegarde les configs dans `ansible-projet4/playbooks/backup/`.


# 15 Serveur web <a id="15"></a>

## 15.1 Serveur web sur une station Ubuntu

Sur le serveur web nous devons d'abord paramétrer une adresse IP fixe cohérente avec le bloque IPv4 choisit pour le réseau de la DMZ : 192.168.10.0/24. Sur Ubuntu nous faisons les modifications d'adressage avec "Netplan": 

	vi /etc/netplan/*.yaml
	network:
	  version: 2
	  renderer: networkd
	  ethernets:
	    eth0:
	      addresses: [192.168.10.1/24]
	      gateway4: 192.168.10.254
	      nameservers:
	              addresses: [1.1.1.1, 8.8.8.8]
	      dhcp4: false
	      dhcp6: false
    # Appliquer les nouveaux réglages et redémarrer networkd
    netplan apply
    systemctl restart systemd-networkd

Nous devons ensuite installer un serveur HTTP sur la machine. Nous utiliserons apache2 pour la simplicitée avec php et mysql.

    apt install apache2 php libapache2-mod-php mysql-server php-mysql
    apt install net-tools
	
    # Démarre le service web apache2
    systemctl restart apache2.service
    # vérifier que le service apache2 est bien sur écoute du port 80
    netstat -antp | grep apache2

## 15.2 Configuration Virtual IP sur Fortigate pour rediriger traffic HTTP et HTTPS

Pour accéder aux pages web présente sur le serveur de la DMZ depuis l'extérieur (WAN) le traffic HTTP arrivant sur le port 3 (192.168.122.29) du parfeu Fortigate (qui fait aussi office de routeur ici) devra être redirigé vers l'adresse 192.168.10.1 sur le port 80.

On utilise une procédure mise à disposition sur le site de Fortrinet.

Référence: [Fortinet Library](https://docs.fortinet.com/document/fortigate/5.4.0/cookbook/361386 "cliquez ici !")

1. Configuring the FortiGate's DMZ interface:

Go to **Network > Interfaces** and edit the DMZ interface.
This example uses the port3 interface as the DMZ interface. The interface Alias indicates that this is the DMZ interface. As well the Role is set to DMZ.
For enhanced security, disable all Administrative Access options.

2. Creating virtual IPs:

Go to **Policy & Objects > Virtual IPs.** Create two virtual IPs: one for HTTP access and one for HTTPS access.
Each virtual IP has the same address, mapping from the Internet to the DMZ interface. The difference is the port for each traffic type: port 80 for HTTP and port 443 for HTTPS.

3. Creating firewall policies:

Go to **Policy & Objects > IPv4 Policy.** Create a firewall policy to allow HTTP and HTTPS traffic from the Internet to the web server. Add both VIPs as the destination address.
Do not enable NAT. Enabling the NAT option actually enables source NAT which is not required for this configuration since the VIPs are added to perform destination NAT. If you do enable source NAT the configuration will still work but all traffic received by the web server will have the same source IP address so you will loose information about your website users.
You can also enable logging for all sessions to make it easier to test the configuration.
Create a second firewall policy to allow HTTP and HTTPS traffic from the internal network to the web server.

4. Results

Internet users and internal network users can access the web server by browsing to the web server's Internet address  http://192.168.122.29. Internal users can also access the web server using its DMZ address (in this example, http://192.168.10.1.
Since only HTTP and HTTPS are enabled, the web server is not accessible using other protocols (such as FTP) and you also cannot ping the web server from the Internet or from the internal network.
Go to FortiView Policies to see current sessions for each firewall policy. If you add a filter to just show policies with the DMZ interface as the destination interface you will see sessions from the Internal network to the web server and from the Internet to the web server.
Double-clicking on the Internet to DMZ web server session shows sessions from Internet addresses and from the internal network.

Test: [serveur web](http://192.168.122.29 "cliquez ici !")

