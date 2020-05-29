## DHCP & DNS

## Configuration du DHCP

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
     
### Configuration du DNS

Comme server DNS nous utilisons le server publique `1.1.1.1` car il est réputé plus confidentiel pour les données. 
Il est configuré sur chaque périphérique réseaux avec la commande:

     ip name-server 1.1.1.1
