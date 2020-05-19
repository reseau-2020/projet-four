'''

 ! Configuration de DS1:
 ! Configuration initiale:

 hostname DS1
 enable secret testtest
 service password-encryption
 ip domain-name lan.project4
 crypto key generate rsa modulus 2048
 ip ssh version 2
 line vty 0 4
 transport input ssh
 login local

 ! Désactiver CDP sur le périphérique
 no cdp run

 ! Création des VLANs:

 interface range g0/0-3,g1/0-3,g2/0-3,g3/0-3
 shutdown

 vlan 10
 name DATA
 vlan 20
 name VOICE
 vlan 30
 name CAMERA
 vlan 40
 name EXECUTIVE
 vlan 99
 name NATIVE 

 ! Création des groupes Etherchannel:
 interface range g0/0,g1/0
  shutdown
  channel-group 1 mode desirable
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

 interface range g0/2,g1/2
  shutdown
  channel-group 3 mode desirable
  switchport trunk encapsulation dot1q
  switchport trunk native vlan 99
  switchport mode trunk
  no shutdown

 interface range g2/1,g3/1
  shutdown
  channel-group 6 mode desirable
  switchport trunk encapsulation dot1q
  switchport trunk native vlan 99
  switchport mode trunk
  no shutdown

 interface range g2/0,g3/0
  shutdown
  channel-group 7 mode desirable
  switchport trunk encapsulation dot1q
  switchport trunk native vlan 99
  switchport mode trunk
  no shutdown

 interface range po1,po3,po5,po6,po7
  shutdown
  switchport trunk encapsulation dot1q
  switchport trunk native vlan 99
  switchport mode trunk
  no shutdown


 ! Configuration de Rapid spanning-tree 
 spanning-tree mode rapid-pvst
 spanning-tree vlan 10,30,99 root primary
 spanning-tree vlan 20,40 root secondary

 ! Configuration IP des interfaces VLAN
 interface vlan 10
  ip address 10.16.10.252 255.255.255.0
  ipv6 address fe80::d1:10 link-local
  ipv6 address fd00:1ab:10::1/64
  ipv6 address 2001:470:c814:4010::1/64
  no shutdown
 interface vlan 20
  ip address 10.16.20.252 255.255.255.0
  ipv6 address fe80::d1:20 link-local
  ipv6 address fd00:1ab:20::1/64
  ipv6 address 2001:470:c814:4020::1/64
  no shutdown
 interface vlan 30
  ip address 10.16.30.252 255.255.255.0
  ipv6 address fe80::d1:30 link-local
  ipv6 address fd00:1ab:30::1/64
  ipv6 address 2001:470:c814:4030::1/64
  no shutdown
 interface vlan 40
  ip address 10.16.40.252 255.255.255.0
  ipv6 address fe80::d1:40 link-local
  ipv6 address fd00:1ab:40::1/64
  ipv6 address 2001:470:c814:4040::1/64
  no shutdown
 ip routing


 ! Configuration du server DHCP:
 ip dhcp pool VLAN10
  network 10.16.10.0 255.255.255.0
  default-router 10.16.10.252
 ! ip dhcp excluded-address 10.16.10.0 10.16.10.0
 ip dhcp pool VLAN20
  network 10.16.20.0 255.255.255.0
  default-router 10.16.20.0
 ! ip dhcp excluded-address 10.16.20.0 10.16.20.0
 ip dhcp pool VLAN30
  network 10.16.30.0 255.255.255.0
  default-router 10.16.30.0
 ! ip dhcp excluded-address 10.16.30.0 10.16.30.0
 ip dhcp pool VLAN40
  network 10.16.40.0 255.255.255.0
  default-router 10.16.40.0
 ip dhcp excluded-address 10.16.40.0 10.16.40.0

'''
