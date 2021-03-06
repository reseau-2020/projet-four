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
    
    privilege exec all level 7 show running-config
    privilege exec level 5 show
    
    ! Activation de aaa
    aaa new-model
    
    ! Ajout d'un serveur radius avec son IPv4 et ports d'authentification
    radius server Radius-server
     address ipv4 10.32.203.3 auth-port 1812 acct-port 1813
     key password

    ! Autorise l'authentification AAA associé au nouveau serveur Radius
    
    aaa authentication login AuthList1 local group radius none
    aaa authorization exec AuthList1 local group radius none
    
    ! Ajoute une interface de connexion vers le serveur Radius
    ip radius source-interface G0/3
    radius-server attribute 6 on-for-login-auth
    
    ! On configure les lines pour s'authentifier en AAA via le groupe radius
    aaa authorization console
    line vty 0 4
    login authentication AuthList1
    authorization exec AuthList1
    exit
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
