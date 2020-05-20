!Désactivation du routage
(config)#no ip routing
exit
wr
!

!configuration intiale du AS2:
conf t
 hostname AS2
 ip domain-name LAN.PROJECT4
 enable secret testtest
 username root secret testtest
 crypto key gen rsa modulus 2048
 ip ssh version 2
 line vty 0 4
 transport input ssh
 login local
exit
line con 0
logging synchronous
end
wr
!

!Configuration de Vlans
conf t
vlan 10
exit
vlan 20
exit
vlan 30
exit
vlan 40
exit
vlan 99
name native
exit
ip default-gateway 10.16.10.254
end
wr

!Configuration des ports "Access": activation de ports des stations de travail
Conf t
interface g2/0
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 spanning-tree bpduguard enable
 no shutdown
interface g2/1
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
 spanning-tree bpduguard enable
 no shutdown
interface g2/2
 switchport mode access
 switchport access vlan 30
 spanning-tree portfast
 spanning-tree bpduguard enable
 no shutdown
interface g2/3
 switchport mode access
 switchport access vlan 40
 spanning-tree portfast
 spanning-tree bpduguard enable
 no shutdown
exit
wr

!Configuration des  ports "trunk"
conf t
interface range g0/0,g1/0
 shutdown
 channel-group 4 mode desirable
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport mode trunk
 no shutdown
interface range g0/1,g1/1
 shutdown
 channel-group 5 mode desirable
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport mode trunk
 no shutdown
interface range po4,po5
 shutdown
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport mode trunk
 no shutdown
exit
wr

!Configuration du spanning-tree
spanning-tree mode rapid-pvst
exit
wr


!Désactivation du CDP
no run cdp 
wr



