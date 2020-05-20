# Configuration de DS2

enable
conf t
hostname DS2
ip domain-name LAN.PROJECT4
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
!8
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
end
wr
!
!
conf t
interface vlan 10
ip address 10.16.10.253 255.255.255.0
no shutdown
exit
interface vlan 20
ip address 10.16.20.253 255.255.255.0
no shutdown
exit
interface vlan 30
ip address 10.16.30.253 255.255.255.0
no shutdown
exit
interface vlan 40
ip address 10.16.40.253 255.255.255.0
no shutdown
exit
ip default-gateway 10.16.10.254
end
wr
!
!
conf t
interface range g0/1, g1/1
shutdown
channel-group 2 mode desirable
switchport trunk encapsulation dot1q
switchport trunk native vlan 99
switchport mode trunk
no shutdown
!
interface range g0/2, g1/2
shutdown
channel-group 3 mode desirable
switchport trunk encapsulation dot1q
switchport trunk native vlan 99
switchport mode trunk
no shutdown
!
interface range g0/0, g1/0
shutdown
channel-group 4 mode desirable
switchport trunk encapsulation dot1q
switchport trunk native vlan 99
switchport mode trunk
no shutdown
!
interface range po2, po3, po4
shutdown
switchport trunk encapsulation dot1q
switchport trunk native vlan 99
switchport mode trunk
no shutdown
exit
!
!
conf t
interface range g2/0, g3/0
shutdown
channel-group 6 mode desirable
switchport trunk encapsulation dot1q
switchport trunk native vlan 99
switchport mode trunk
no shutdown
!
interface range g2/1, g3/1
shutdown
channel-group 7 mode desirable
switchport trunk encapsulation dot1q
switchport trunk native vlan 99
switchport mode trunk
no shutdown
exit
!
end
wr
!
!
conf t
spanning-tree vlan 20, 40 root primary
spanning-tree vlan 10, 30 root secondary
spanning-tree mode rapid-pvst
end
wr
!
