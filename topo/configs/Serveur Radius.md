# Gestion des accès aux routeurs via un serveur Radius
## Création du serveur freeRadius sur un terminal Ubuntu

On a choisit de rajouter un pc ubuntu sur le switch relié a R3 pour gérer les authentification de R1 R2 R3. 

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

On ajoute ensuite les utilisateurs enregistrés sur les clients ainsi que leur mot de passe dans un deuxième fichier. On fixe le niveau de privilège (15=max).

    vi users
    root Cleartext-Password := "testtest"
     Service-Type = NAS-Prompt-User,
     Cisco-AVPair = "shell:priv-lvl=15"

## Configuration des routeurs R1 R2 R3 comme clients Radius

    ! Activation de aaa
    aaa new-model
    ! Ajout d'un serveur radius avec son IPv4 et ports d'authentification
    radius server Radius-server
    address ipv4 10.32.203.3 auth-port 1812 acct-port 1813
    key password

    ! Autorise l'authentification AAA associer au nouveau serveur Radius
    aaa authentication login default group radius local

## Diagnostics

    show run | in radius
    aaa authentication login default group radius local
    radius server Radius-server

    show run | in aaa
    aaa new-model
    aaa authentication login default group radius local
    aaa session-id common
    snmp-server enable traps aaa_server
