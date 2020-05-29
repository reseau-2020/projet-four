# VPN IPsec site-à-site


Pour sécuriser la connexion entre les 2 sites distants nous avons configuré un tunnel VPN IPsec. 
Le tunnel VPN permet de créer un lien direct entre des réseaux distants et d'isoler leurs échanges du reste du trafic sur le réseau publique.
Le protocole IPsec permet lui d'authentifier et de chiffrer les données, ainsi le flux n'est compréhensible que par le destinataire et ne peut être modifié.
C'est ce protocole qui apporte l'aspect sécurité du tunnel.

Pour être fonctionnel le tunnel doit être configuré sur les 2 sites distants, nous l'avons donc déployé sur le pare-feu Fortigate et également sur le routeur CISCO R1.

## Configuration sur Fortigate

Côté fortigate on utilise l'interface web du pare-feu en se connectant via l'adresse IP d'une des interfaces. 
Dans le menu `VPN --> IPsec Wizard` on peut déployer un tunnet "par défault" en suivant les 3 étapes de l'assistant:

1.VPN Setup :
    - Nom : 'Branch-to-HQ'
    - Template Type : Site-to-Site
    - Remote device Type : CISCO
    - NAT Configuration : No NAT between sites
    
2.Authentification :
    - Remote Device : IP Address
    - IP Address : 192.168.122.18
    - Outgoing interface : port3
    - Authentication : Pre-shared key (********)
    
3.Policy&Routing:
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

## Configuration du VPN sur le routeur R1

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
