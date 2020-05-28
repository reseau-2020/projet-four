# 3 Les VLANs

Pour segmenter logiquement le réseau de la couche Access nous avons créer 4 VLANs pour 4 types d'utilisateurs différents :

* VLAN 10 : DATA
* VLAN 20 : VOICE
* VLAN 30 : CAMERA
* VLAN 40 : EXECUTIVE

La configuration des VLANs permettent de résoudre plusieurs problèmes :

1. La sécurité : les VLANs permettent d'isoler les flux de données en fonction des utilisateurs (interfaces) mais aussi d'isoler certaines parties du réseau (server) sans recours à un routeur.
2. L'optimisation : avec une segmentation logique on peut créer plusieurs réseaux sans avoir besoin d'ajouter des switchs et des câbles
3. Qualité de service : On peut réserver de la bande passante pour certains usages (VoIP)

## Configuration

On commence par créer et nommer les différentes VLANs sur les périphériques des couches Access et Distribution (DS1&2, AS1&2):

    vlan 10
    name DATA
    ...

Les interfaces physiques sur lesquelles le trafics de plusieurs vlans doit passer seront monter en mode trunk en ajoutant le protocole d'encapsulation dot1q (IEEE 802.1q).
Ce standard permet de modifier les trames Ethernet pour fournir un mécanisme d'encapsulation qui permet de faire passer le traffic de plusieurs VLANs sur un lien physique.
Le VLAN 99 sera le Vlan Natif, il sera utilisé pour le transport des trames ethernet non taggés sur les interfaces en mode trunk.

Le trunking est activé sur les interfaces de liaison entre la couche Access et Distribution (AS --> DS) mais aussi sur les interfaces de liaisons entre DS1 et DS2 qui assurent une redondance de liens.

    interface range g0/0,g1/0
     switchport trunk encapsulation dot1q     ! --> On active le protocole dot1q
     switchport trunk native vlan 99          ! --> On renseigne le VLAN natif
     switchport mode trunk                    ! --> On force le passage du mode DTP à "ON" pour activer le trunking
     no shutdown

On configure ensuite les interfaces virtuelles VLAN que l'on a créee sur différentes plages d'adresses IPv4 et IPv6.
Dans notre topologie on a choisit de faire varier le troisième octet du bloque d'adresses IPv4 pour différentier logiquement les VLANs.

        |VLAN | Adresses ipv4  |  Adresses ipv6
        |-----|----|----|
        | VLAN10 | `10.16.10.0/24` | `fe80::d1:10` ; `fd00:1ab:10::1` ; `2001:470:c814:4011::`
        | VLAN20 | `10.16.20.0/24` | `fe80::d1:20` ; `fd00:1ab:20::1` ; `2001:470:c814:4021::` 
        | VLAN30 | `10.16.30.0/24` | `fe80::d1:30` ; `fd00:1ab:30::1` ; `2001:470:c814:4031::`
        | VLAN40 | `10.16.40.0/24` | `fe80::d1:40` ; `fd00:1ab:40::1` ; `2001:470:c814:4041::`


