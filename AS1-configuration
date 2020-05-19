!
enable
conf t
hostname AS1
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
conf t
vlan 10
exit
vlan 20
exit
vlan 30
exit
vlan 40
exit
vlan 99vl
name native
exit
int vlan10
ip add 10.16.10.1 255.255.255.0
exit
ip default-gateway 10.16.10.254
end
wr
!
conf t
interface range g2/0
switchport mode access
switchport access vlan 10
spanning-tree portfast
spanning-tree bpduguard enable
exit
interface range g2/1 
switchport mode access
switchport access vlan 20
spanning-tree portfast
spanning-tree bpduguard enable
exit
interface range g2/2
switchport mode access
switchport access vlan 30
spanning-tree portfast
spanning-tree bpduguard enable
exit
interface range g2/3
switchport mode access
switchport access vlan 40
spanning-tree portfast
exit
!
conf t
interface range g0/0, g1/0
shutdown
channel-group 1 mode desirable
switchport trunk encapsulation dot1q
switchport trunk native vlan 99
switchport mode trunk
no shut
interface range g0/1,g1/1
shutdown
channel-group 2 mode desirable
switchport trunk encapsulation dot1q
switchport trunk native vlan 99
switchport mode trunk
no shutdown
interface range po1,po2
shutdown
switchport trunk encapsulation dot1q
switchport trunk native vlan 99
switchport mode trunk
no shutdown
exit
end
wr
