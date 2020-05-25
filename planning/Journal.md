# Jour1: 18/05/2020
Pour ce premier jour de démarrage, on a repris l’énoncé du projet avec son cahier de charge et en fonction on a listé les tâches et élaboré un Digramme de GANT. 
Ensuite on s’est intéressé au plan d’adressage IPV4 et IPV6.

# Jour2: 19/05/2020

Tâches réalisées aujourd’hui:
-	Faire le point avec François concernant le plan d’adressage 
-	Continuer sur l’adressage IPv6
-	Validation du plan d’adressage avec François
-	Faire le point sur la topo sur GNS3
-	Répartir les tâches sur les membres de l’équipe
-	Configuration de DS1, DS2, AS1 et AS2 (hostname, ssh, vlan, port trunk et access, spanning-tree)

Tâches à réaliser pour demain:
- Continuer la configuration sur GNS3
- S'assurer que la topo est opérationnelle 

# Jour 3 : 20/05/2020
On a commencé la configuration de la couche core des routeurs.
On a choisi le protocole de routage EIGRP, plus facile à implémenter.

Tâches réalisées aujourd’hui :
- finalisation de la config de DS1 & DS2 (HSRPv4, HSRPv6, eigrpv4, eigrpv6, DHCP) (Clément, Francois)
- configuration des routeurs (eigrpv4, eigrpv6, nat) (Asma et Besma)
- rectification du plan d'adressage

Tâches à réaliser pour 22/02/2020 :
- rectifier la config de routeurs R2 et R1
- tester les connectivités à l'intérieur du LAN
- tester les connectivités à l'internet

# Jour 4 : 22/05/2020
Tâches réalisées aujourd’hui
-	Finir la configuration de trois routeurs,
-	Implémenter le Nat sur R1
-	Tester la connectivité
-	Mise en œuvre d’un pare-feu Cisco sur R1
-	Mise en œuvre d’une zone DMZ 
-	Mise en place d’un site distant connecté en VPN IPSEC

Tâches à réaliser pour 25/05/2020
-	Implémenter NTP, le syslog et SNMP
-	Elaborer un cas qui éprouve la fiabilité de la solution et un autre qui éprouve la sécurité de la solution
-	Partir sur ansible


# Jour 5 : 25/05/2020
Tâches réalisées aujourd’hui

- Asma et Besama ont configuré SYSLOG, SNMP et NTP sur les périphériques
	-	Configuration de NTP sur le tripod et les switchs
	-	Configuration de SNMP sur le triod
	-	Configuration de Syslog
- Clément et François ont finalisé le tunnel VPN entre le site distant (pare-feu fortinet) et le site central (pare-feu Cisco). Connexion en ssh réusssie

Tâches à réaliser pour 26/05/2020

- Tester la topologie avec un cas fiablité et un cas séxurité
- Ajuster les configs si nécessaire
