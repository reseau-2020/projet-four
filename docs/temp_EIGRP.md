# 8 EIGRP

Pour le routage entre la couche Distribution et la couche Core nous avons choisi d'utiliser le protocole de routage dynamique EIGRP notamment pour sa facilité de déploiement (vs OSPF) en IPv6.
EIGRP était un IGP propriétaire CISCO mais depuis 2013 il est devenu un standard de l'IETF partiellement ouvert.
Il utilise un protocole à vecteur de distances IP avec une distance administrative en interne de 90.

## 1. Configuration

Le routage EIGRP est activé sur les routeurs R1, R2, R3 et sur les commutateurs de couche 3 DS1 et DS2 sur le système autonome AS 1.
Un router-ID est associé à chaque routeur (1.1.1.1, 2.2.2.2,...) pour les différencier. Les interfaces qui ne participent pas au routage dynamique en local (interfaces VLAN ou vers internet) seront ajoutés
en passive-interface. Tous les réseaux adjacent au périphérique sont ajoutés au système autonome. On ajoute la commande "no auto-summary" pour ne pas agréger les routes dans la table de routage.
La route par défaut (vers internet) est distribuée par R1 en activant la commande "Redistribute static"

_Exemple sur R2:_

    !Activation de routage en ipv4
    router eigrp 1
     passive-interface g0/0
     eigrp router-id 2.2.2.2
     no auto-summary
     !Ajout des réseaux adjacents
     network 10.32.202.0
     network 10.32.12.0
     network 10.16.214.0
     network 10.32.23.0
     network 10.16.224.0
     network 10.16.215.0
     network 10.16.225.0
     
## 2. Vérification

Pour déboguer les erreurs EIGRP on peut utiliser les commandes suivantes :

    show ip protocols           ! --> Vérifier si le protocol est bien activer, voir network/passive interface
    show ip eigrp neighbors     !--> Voir le voisinage du routeur en EIGRP avec Uptime/hold
    show ip eigrp topology      !--> Voir la topology du réseau avec interfaces et adresses IP des autres routeurs
    show ip route               !--> Voir toute la table de routage, les routes dynamique EIGRP sont symbolisés par la lettre D

  
