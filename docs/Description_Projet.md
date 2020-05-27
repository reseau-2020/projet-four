# Documentation générale du projet 4

Ce document présente globalement ce que nous avons mis en place grace au logiciel open source *GNS3*. Nous y décrirons les périphériques employés ainsi que les protocoles utilisés.

## 1 Topologie

![Capture GNS3](https://github.com/reseau-2020/projet-four/tree/master/topo/topologie.png?raw=True)

## 2 Plan d'adressage
### IPv4
Le plan d'adressage de notre topologie est accessible ici *https://github.com/reseau-2020/projet-four/blob/master/topo/plan_adressage.md*. Nous avons utilisé des adresses en `10.32.X.X` pour les liaisons interne à la couche *CORE* et en `10.16.X.X` pour les liaisons entre les liaisons impliquant les couches *DISTRIBUTION* et *ACCESS*. Chaque sous-réseau possède un masque égal à 255.255.255.0. Le troisième octet des adresses renseigne sur la liaison entre les périphériques concernés. Par exemple, les routeurs *R1* et *R2* sont reliés en `10.32.12.1` (sur R1) et `10.32.12.2` (sur R2). On assigne 4 à *DS1* et 5 à *DS2*, ainsi *R3* et *DS2* sont reliés par `10.16.135.1` et `10.16.235.2` (sur *R3*), `10.16.135.2` et `10.16.235.1` (sur *DS2*).
Les *VLANs 10, 20, 30 et 40* prennent les adresses `10.32.10.X`, `10.32.20.X`, `10.32.30.X` et `10.32.40.X`.
Pour le site distant nous avons utilisé des adresses privées en `192.168.150.X`.

### Ipv6
L'adressage IPv6

## 3 VLAN
## 4 Spanning-tree
## 5 Etherchannel
## 6 HSRP
## 7 DHCP & DNS
## 8 EIGRP
## 9 NAT
## 10 IPv6
## 11 Pare-feux & VPN IPsec
### Pare-feux
Nous avons mis en place deux pare-feux : un ZBF de Cisco sur *R1* dans le site principal et un pare-feu fortigate dans le site distant.
Sur le Cisco nous avons créé trois zone :
- Internet : `zone security lan`
- Lan : `zone security internet`
- DMZ : `zone security dmz`

Succintement, les protocoles autorisés entre zones sont : 
- lan -> internet :  http, https, dns, icmp, ssh
- lan -> dmz : http, https, ssh, icmp
- internet -> dmz : http, https
- dmz -> internet :  http, https, dns, icmp, ssh
 
### VPN
Nous avons monté un tunnel entre les deux sites via une authentification `esp-des` et un encryptage `esp-md5-hmac`. La différence des pare-feux de chaque côtés ainsi que les versions limitées offertes par *GNS3* ne nous ont pas permis d'avoir un tunnel 100% efficace. Il se monte bien dans le sens **Site Principal** => **Site Distant**, mais pas inversement.

## 12 SNMP
## 13 SYSLOG
## 14 NTP
## 15 Radius
## 16 Sécurité
## 17 Fiabilité

