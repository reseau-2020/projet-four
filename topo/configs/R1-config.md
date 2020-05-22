```
!Configuration des routeurs
conf t
hostname R1
username root secret testtest
ip domain-name LAN.PROJECT4
crypto key gen rsa modulus 2048
ip ssh version 2
line vty 0 4
transport input ssh
login local
exit
line con 0
logging synchronous

!Mise en place IPv6 / IPv4

ipv6 unicast-routing

interface Loopback0
 ip address 1.1.1.1 255.255.255.255
!
interface GigabitEthernet0/0
 no shutdown
 ip address 10.32.201.1 255.255.255.0
 ipv6 address FE80::1 link-local
 ipv6 address FD00:FD00:FD00:2::1/64
 ipv6 address 2001:470:c814:4001::2/64
 ipv6 eigrp 1

!
interface GigabitEthernet0/1
 no shutdown
 ip address 10.32.32.1 255.255.255.0
 ipv6 address FE80::1:cafe:4 link-local
 ipv6 eigrp 1
!
interface GigabitEthernet0/2
 no shutdown
 ip address 10.32.12.1 255.255.255.0
 ipv6 address FE80::1 link-local
 ipv6 eigrp 1
!
interface GigabitEthernet0/3
 no shutdown
 ip address 10.32.13.1 255.255.255.0
 ipv6 address FE80::1 link-local
 ipv6 eigrp 1

!EIGRP
!Routage IPv6
ipv6 router eigrp 1
 passive-interface GigabitEthernet0/0
 eigrp router-id 1.1.1.1

!Routage IPv4
 router eigrp 1
 passive-interface GigabitEthernet0/0
 eigrp router-id 1.1.1.1
 network 10.32.201.0
 network 10.32.12.0
 network 10.32.13.0
 redistribute static
end
wr

!implémentation du nat
ip access-list standard lan
permit 10.32.201.0 0.0.255.255
permit 10.32.12.0 0.0.255.255
permit 10.32.13.0 0.0.255.255
exit
!
ip nat inside source list lan interface G0/1 overload
no ip nat inside source list lan interface G0/0 overload
no ip nat inside source list lan interface G0/2 overload
no ip nat inside source list lan interface G0/3 overload
!
int g0/0
ip nat inside
int g0/2
ip nat inside
int g0/3
ip nat inside
int g0/1
ip nat outside


ip route 10.0.0.0 255.0.0.0 192.168.122.1
```
