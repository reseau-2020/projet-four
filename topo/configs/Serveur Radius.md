
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
