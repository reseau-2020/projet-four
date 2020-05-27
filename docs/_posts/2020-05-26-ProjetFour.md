---
layout: post
title:  "Récapitulatif du mardi 26 mai"
date:   2022-05-26
categories: welcome
---

# Jour 6 : 26/05/2020

Tâches réalisées aujourd’hui

- Connexion en ipv6 : configuration de DHCPv6 Statefull sur DS1/DS2, ajout adresse server DNS IPv6, en EIGRPv6 prise en compte des interfaces vlan sur DS1/DS2 (mode passif) et ajout de la commande "redistribute static" sur R1 uniquement, et G0/1 passive-interface 
- Tests de connectivité en ipv4 et ipv6 : ping -6 depuis la couche access vers la couche core via les adresses privée et publique, ping -6 vers l'internet
- Finalisation et vérification de SNMP et de syslog (qq pb car on avait mis le serveur snmp dans la dmz)

Tâches à réaliser pour 27/05/2020

- Régler les bugs
- Etudier la fiabilité et l'aspect sécuritaire de la topo
- Sauvgarder la config avec Ansible
