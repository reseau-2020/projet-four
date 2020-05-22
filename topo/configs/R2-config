'''
!Configuration initiale
conf t
 hostname R2
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

! Configuration des interfaces et activation de routage en ipv6
interface Loopback0
 ip address 2.2.2.2 255.255.255.255
!
ipv6 unicast-routing
!
interface g0/0
 no shutdown
 ip address 10.32.202.2 255.255.255.0
 ipv6 address fe80::2 link-local
 ipv6 address 2001:470:c814:4002::2:1
 ipv6 address fd00:fd00:fd00:2::2:1
 ipv6 eigrp 1
!
interface g0/1
 no shutdown
 ip address 10.32.12.2 255.255.255.0
 ipv6 address fe80::2 link-local
 ipv6 eigrp 1
!
interface g0/2 
 no shutdown
 ip address 10.16.214.1 255.255.255.0
 ipv6 address fe80::2 link-local
 ipv6 eigrp 1 
!
interface g0/3
 no shutdown
 ip address 10.32.23.1 255.255.255.0
 ipv6 address fe80::2 link-local
 ipv6 eigrp 1 
!
interface g0/4
 no shutdown
 ip address 10.16.224.2 255.255.255.0
 ipv6 address fe80::2 link-local
 ipv6 eigrp 1
!
interface g0/5
 no shutdown
 ip address 10.16.215.1 255.255.255.0
 ipv6 address fe80::2 link-local
 ipv6 eigrp 1
!
interface g0/6
 no shutdown
 ip address 10.16.225.2 255.255.255.0
 ipv6 address fe80::2 link-local
 ipv6 eigrp 1
!
ipv6 unicast-routing
ipv6 router eigrp 1
 passive-interface g0/0
 eigrp router-id 3.3.3.3

!Activation de routage en ipv4
router eigrp 1
 passive-interface g0/0
 eigrp router-id 2.2.2.2
 network 10.32.202.0
 network 10.32.12.0
 network 10.16.214.0
 network 10.32.23.0
 network 10.16.224.0
 network 10.16.215.0
 network 10.16.225.0
 end
