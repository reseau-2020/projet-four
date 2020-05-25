! Configuration de DS1:

! Configuration initiale et connexion aux consoles :

    hostname DS1
    ip domain-name lan.project4
    username root algorithm-type sha256 secret testtest
    service password-encryption
    crypto key generate rsa modulus 2048
    ip ssh version 2
    line vty 0 4
    transport input ssh
    login local
    exit
    line con 0
    logging synchronous

! Désactiver CDP sur le périphérique

    no cdp run

! Configuration serveur de nom:

    ip name-server 1.1.1.1
    ntp server pool.ntp.org

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

    interface range g0/2,g1/2
     shutdown
     channel-group 3 mode desirable
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

    interface range po1,po3,po5
     shutdown
     switchport trunk encapsulation dot1q
     switchport trunk native vlan 99
     switchport mode trunk
     no shutdown


! Configuration interfaces vers R2 et R3

    interface g3/0
    no switchport
    ip add 10.16.224.1 255.255.255.0
    ipv6 address fe80::d:1 link-local
    no shutdown
    interface g2/0
    no switchport
    ip add 10.16.214.2 255.255.255.0
    ipv6 address fe80::d:1 link-local
    no shutdown
    interface g3/1
    no switchport
    ip add 10.16.234.1 255.255.255.0
    ipv6 address fe80::d:1 link-local
    no shutdown
    interface g2/1
    no switchport
    ip add 10.16.134.2 255.255.255.0
    ipv6 address fe80::d:1 link-local
    no shutdown
    exit

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
     default-router 10.16.10.254
     dns-server 1.1.1.1
     ip dhcp excluded-address 10.16.10.128 10.16.10.255
    ip dhcp pool VLAN20
     network 10.16.20.0 255.255.255.0
     default-router 10.16.20.254
     dns-server 1.1.1.1
     ip dhcp excluded-address 10.16.20.128 10.16.20.255
    ip dhcp pool VLAN30
     network 10.16.30.0 255.255.255.0
     default-router 10.16.30.254
     dns-server 1.1.1.1
     ip dhcp excluded-address 10.16.30.128 10.16.30.255
    ip dhcp pool VLAN40
     network 10.16.40.0 255.255.255.0
     default-router 10.16.40.254
     dns-server 1.1.1.1
     ip dhcp excluded-address 10.16.40.128 10.16.40.255

! Configuration HSRP

    interface vlan 10
     standby 10 ip 10.16.10.254
     standby 10 priority 150
     standby 10 preempt
     standby version 2
     standby 16 ipv6 fe80::d10
     standby 16 priority 150

    interface vlan 20
     standby 20 ip 10.16.20.254
     standby version 2
     standby 26 ipv6 fe80::d20
    
    interface vlan 30
     standby 30 ip 10.16.30.254
     standby 30 priority 150
     standby 30 preempt
     standby version 2
     standby 36 ipv6 fe80::d30
     standby 36 priority 150
    
    interface vlan 40
     standby 40 ip 10.16.40.254
     standby version 2
     standby 46 ipv6 fe80::d40
    end


! Configuration EIGRP

    router eigrp 1
     passive-interface GigabitEthernet3/3
     passive-interface vlan 10
     passive-interface vlan 20
     passive-interface vlan 30
     passive-interface vlan 40
     eigrp router-id 10.10.10.10
     no auto-summary
     network 10.16.1.0 0.0.0.255
     network 10.16.2.0 0.0.0.255
     network 10.16.3.0 0.0.0.255
     network 10.16.4.0 0.0.0.255
     network 10.32.42.0 0.0.0.255
     network 10.32.43.0 0.0.0.255
     network 10.32.44.0 0.0.0.255
     network 10.32.45.0 0.0.0.255
     network 10.16.10.0 0.0.0.255
     network 10.16.20.0 0.0.0.255
     network 10.16.30.0 0.0.0.255
     network 10.16.40.0 0.0.0.255

! Configuration EIGRP IPv6
    
    ipv6 unicast-routing
    ipv6 router eigrp 1
     eigrp router-id 10.10.10.10
     passive-interface GigabitEthernet3/3
     passive-interface vlan 10
     passive-interface vlan 20
     passive-interface vlan 30
     passive-interface vlan 40

    interface GigabitEthernet3/0
     ipv6 eigrp 1
    interface GigabitEthernet2/0
     ipv6 eigrp 1
    interface GigabitEthernet3/1
     ipv6 eigrp 1
    interface GigabitEthernet2/1
     ipv6 eigrp 1
