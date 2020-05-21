# Configuration de DS2
======================
```
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
!
! VLANs
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
vlan 99
name native
exit
end
wr
!
conf t
interface vlan 10
ip address 10.16.10.253 255.255.255.0
ipv6 address fe80::d2:10 link-local
ipv6 address fd00:1ab:10::2/64
ipv6 address 2001:471:c814:4010::2/64
no shutdown
exit
interface vlan 20
ip address 10.16.20.253 255.255.255.0
ipv6 address fe80::d2:20 link-local
ipv6 address fd00:1ab:20::2/64
ipv6 address 2001:471:c814:4020::2/64
no shutdown
exit
interface vlan 30
ip address 10.16.30.253 255.255.255.0
ipv6 address fe80::d2:30 link-local
ipv6 address fd00:1ab:30::2/64
ipv6 address 2001:471:c814:4030::2/64
no shutdown
exit
interface vlan 40
ip address 10.16.40.253 255.255.255.0
ipv6 address fe80::d2:40 link-local
ipv6 address fd00:1ab:40::2/64
ipv6 address 2001:471:c814:4040::2/64
no shutdown
exit
ip default-gateway 10.16.10.254
end
wr
!
! Etherchannel
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
end
wr
!
! LINK TO R2 & R3
!
conf t
int g2/1
no switchport
ip add 10.16.215.2 255.255.255.0
no shut
int g3/1
no switchport
ip add 10.16.225.1 255.255.255.0
no shut
int g2/0
no switchport
ip add 10.16.135.2 255.255.255.0
no shut
int g3/0
no switchport
ip add 10.16.235.1 255.255.255.0
no shut
end
wr
!
! Spanning-tree
!
conf t
spanning-tree vlan 20, 40 root primary
spanning-tree vlan 10, 30 root secondary
spanning-tree mode rapid-pvst
end
wr
!
! HSRP
!
conf t
interface vlan 10
standby 10 ip 10.16.10.254
exit
interface vlan 20
standby 20 ip 10.16.20.254
standby 20 priority 150
standby 20 preempt
exit
interface vlan 30
standby 30 ip 10.16.30.254
exit
interface vlan 40
standby 40 ip 10.16.40.254
standby 40 priority 150
standby 40 preempt
end
wr
!
! HSRP v6
!
conf t
interface vlan 10
standby version 2
standby 16 ipv6 fe80::d10
exit
interface vlan 20
standby 26 priority 150
standby 26 preempt
standby version 2
standby 26 ipv6 fe80::d20
exit
interface vlan 30
standby version 2
standby 36 ipv6 fe80::d30
exit
interface vlan 40
standby 46 priority 150
standby 46 preempt
standby version 2
standby 46 ipv6 fe80::d40
end
wr
!
! DHCP
!
conf t
ip dhcp pool VLAN10
network 10.16.10.0 255.255.255
default-router 10.16.10.253
exit
ip dhcp pool VLAN20
network 10.16.20.0 255.255.255.0
default-router 10.16.20.253
exit
ip dhcp pool VLAN30
network 10.16.30.0 255.255.255.0
default-router 10.16.30.253
exit
ip dhcp pool VLAN40
network 10.16.40.0 255.255.255.0
default-router 10.16.40.253
exit
ip dhcp excluded-address 10.16.10.1 10.16.10.127
ip dhcp excluded-address 10.16.20.1 10.16.20.127
ip dhcp excluded-address 10.16.30.1 10.16.30.127
ip dhcp excluded-address 10.16.40.1 10.16.40.127
!
! EIGRP
!
conf t
router eigrp 1
passive-interface GigabitEthernet3/3
passive-interface vlan 10
passive-interface vlan 20
passive-interface vlan 30
passive-interface vlan 40
eigrp router-id 5.5.5.5
network 10.16.10.0
network 10.16.20.0
network 10.16.30.0
network 10.16.40.0
network 10.16.52.1
network 10.16.53.1
network 10.16.54.1
network 10.16.55.1
exit
!
! EIGRPv6
!
conf t
ipv6 unicast-routing
interface loopback0
ip address 1.1.1.1 255.255.255.255
ipv6 router eigrp 1
eigrp router-id 5.5.5.5
passive-interface vlan 10
passive-interface vlan 20
passive-interface vlan 30
passive-interface vlan 40
interface g2/0
ipv6 eigrp 1
interface g2/1
ipv6 eigrp 1
interface g3/0
ipv6 eigrp 1
interface g3/1
ipv6 eigrp 1
exit
end
wr
```
