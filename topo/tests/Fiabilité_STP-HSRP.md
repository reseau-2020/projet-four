````
! Vérification de la redondance STP et HSRP:
  
1) Ping continu du pc1 du VLAN 10 vers sa passerelle DS1 avec rupture de la liaison Po1. 
A noter que cette épreuve ne vérifie que l’oeuvre de Spanning-Tree et non celle de HSRP.

[root@pc1 ~]# ping 10.16.10.254
PING 10.16.10.254 (10.16.10.254) 56(84) bytes of data.
64 bytes from 10.16.10.254: icmp_seq=1 ttl=255 time=4.34 ms
64 bytes from 10.16.10.254: icmp_seq=2 ttl=255 time=4.09 ms
64 bytes from 10.16.10.254: icmp_seq=3 ttl=255 time=4.41 ms
64 bytes from 10.16.10.254: icmp_seq=4 ttl=255 time=3.30 ms
64 bytes from 10.16.10.254: icmp_seq=5 ttl=255 time=4.08 ms
64 bytes from 10.16.10.254: icmp_seq=6 ttl=255 time=4.16 ms
64 bytes from 10.16.10.254: icmp_seq=7 ttl=255 time=4.06 ms
64 bytes from 10.16.10.254: icmp_seq=8 ttl=255 time=4.48 ms
64 bytes from 10.16.10.254: icmp_seq=9 ttl=255 time=5.24 ms
64 bytes from 10.16.10.254: icmp_seq=10 ttl=255 time=4.25 ms 
!on fait tomber po1 sur DS1, le délai éprouvé est celui de RSTP (paquets perdus)
From 10.16.10.130 icmp_seq=46 Destination Host Unreachable
From 10.16.10.130 icmp_seq=47 Destination Host Unreachable
From 10.16.10.130 icmp_seq=48 Destination Host Unreachable
From 10.16.10.130 icmp_seq=49 Destination Host Unreachable
From 10.16.10.130 icmp_seq=50 Destination Host Unreachable
From 10.16.10.130 icmp_seq=51 Destination Host Unreachable
From 10.16.10.130 icmp_seq=52 Destination Host Unreachable
From 10.16.10.130 icmp_seq=53 Destination Host Unreachable
From 10.16.10.130 icmp_seq=54 Destination Host Unreachable
From 10.16.10.130 icmp_seq=55 Destination Host Unreachable
From 10.16.10.130 icmp_seq=56 Destination Host Unreachable
From 10.16.10.130 icmp_seq=57 Destination Host Unreachable
From 10.16.10.130 icmp_seq=58 Destination Host Unreachable
From 10.16.10.130 icmp_seq=59 Destination Host Unreachable
From 10.16.10.130 icmp_seq=60 Destination Host Unreachable
From 10.16.10.130 icmp_seq=61 Destination Host Unreachable
From 10.16.10.253 icmp_seq=62 Redirect Host(New nexthop: 10.16.10.254) 
! La passerelle du VLAN 10 est maintenant joignable via chemin sous-opGmal par DS2
From 10.16.10.253: icmp_seq=62 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=62 ttl=255 time=16.2 ms
64 bytes from 10.16.10.254: icmp_seq=63 ttl=255 time=6.55 ms
From 10.16.10.253 icmp_seq=64 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=64 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=64 ttl=255 time=8.21 ms
64 bytes from 10.16.10.254: icmp_seq=65 ttl=255 time=6.44 ms
From 10.16.10.253 icmp_seq=66 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=66 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=66 ttl=255 time=10.1 ms
64 bytes from 10.16.10.254: icmp_seq=67 ttl=255 time=6.50 ms
From 10.16.10.253 icmp_seq=68 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=68 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=68 ttl=255 time=7.77 ms
64 bytes from 10.16.10.254: icmp_seq=69 ttl=255 time=5.48 ms
From 10.16.10.253 icmp_seq=70 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=70 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=70 ttl=255 time=6.70 ms
64 bytes from 10.16.10.254: icmp_seq=71 ttl=255 time=7.29 ms
From 10.16.10.253 icmp_seq=72 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=72 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=72 ttl=255 time=7.80 ms
64 bytes from 10.16.10.254: icmp_seq=73 ttl=255 time=6.33 ms
From 10.16.10.253 icmp_seq=74 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=74 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=74 ttl=255 time=8.97 ms
64 bytes from 10.16.10.254: icmp_seq=75 ttl=255 time=4.83 ms
From 10.16.10.253 icmp_seq=76 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=76 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=76 ttl=255 time=7.73 ms
64 bytes from 10.16.10.254: icmp_seq=77 ttl=255 time=5.69 ms
From 10.16.10.253 icmp_seq=78 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=78 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=78 ttl=255 time=7.93 ms
64 bytes from 10.16.10.254: icmp_seq=79 ttl=255 time=6.14 ms
From 10.16.10.253 icmp_seq=80 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=80 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=80 ttl=255 time=9.06 ms
64 bytes from 10.16.10.254: icmp_seq=81 ttl=255 time=5.80 ms
From 10.16.10.253 icmp_seq=82 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=82 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=82 ttl=255 time=7.99 ms
64 bytes from 10.16.10.254: icmp_seq=83 ttl=255 time=5.13 ms
From 10.16.10.253 icmp_seq=84 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=84 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=84 ttl=255 time=8.45 ms
64 bytes from 10.16.10.254: icmp_seq=85 ttl=255 time=6.15 ms
From 10.16.10.253 icmp_seq=86 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=86 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=86 ttl=255 time=9.90 ms
64 bytes from 10.16.10.254: icmp_seq=87 ttl=255 time=5.38 ms
From 10.16.10.253 icmp_seq=88 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=88 Redirect Host(New nexthop: 10.16.10.254)
64 bytes from 10.16.10.254: icmp_seq=88 ttl=255 time=8.37 ms
64 bytes from 10.16.10.254: icmp_seq=89 ttl=255 time=6.07 ms
From 10.16.10.253 icmp_seq=90 Redirect Host(New nexthop: 10.16.10.254)
From 10.16.10.253: icmp_seq=90 Redirect Host(New nexthop: 10.16.10.254) 
64 bytes from 10.16.10.254: icmp_seq=90 ttl=255 time=6.96 ms  ! on remonte le po1 (paquets perdus)
From 10.16.10.130 icmp_seq=102 Destination Host Unreachable
From 10.16.10.130 icmp_seq=103 Destination Host Unreachable
From 10.16.10.130 icmp_seq=104 Destination Host Unreachable
From 10.16.10.130 icmp_seq=105 Destination Host Unreachable
From 10.16.10.130 icmp_seq=106 Destination Host Unreachable
From 10.16.10.130 icmp_seq=107 Destination Host Unreachable
From 10.16.10.130 icmp_seq=108 Destination Host Unreachable
From 10.16.10.130 icmp_seq=109 Destination Host Unreachable
From 10.16.10.130 icmp_seq=110 Destination Host Unreachable
From 10.16.10.130 icmp_seq=111 Destination Host Unreachable
From 10.16.10.130 icmp_seq=112 Destination Host Unreachable
From 10.16.10.130 icmp_seq=113 Destination Host Unreachable
From 10.16.10.130 icmp_seq=114 Destination Host Unreachable
From 10.16.10.130 icmp_seq=115 Destination Host Unreachable
From 10.16.10.130 icmp_seq=116 Destination Host Unreachable
From 10.16.10.130 icmp_seq=117 Destination Host Unreachable
64 bytes from 10.16.10.254: icmp_seq=118 ttl=255 time=6.14 ms ! le DS1 est de nouveau la passerelle de vlan 10
64 bytes from 10.16.10.254: icmp_seq=119 ttl=255 time=4.46 ms
64 bytes from 10.16.10.254: icmp_seq=120 ttl=255 time=4.13 ms
64 bytes from 10.16.10.254: icmp_seq=121 ttl=255 time=4.04 ms
64 bytes from 10.16.10.254: icmp_seq=122 ttl=255 time=3.91 ms
64 bytes from 10.16.10.254: icmp_seq=123 ttl=255 time=4.02 ms
64 bytes from 10.16.10.254: icmp_seq=124 ttl=255 time=4.20 ms
64 bytes from 10.16.10.254: icmp_seq=125 ttl=255 time=3.96 ms

--- 10.16.10.254 ping statistics ---
125 packets transmitted, 47 received, +47 errors, 62% packet loss, time 124077ms
rtt min/avg/max/mdev = 3.305/6.244/16.256/2.315 ms, pipe 4

------------------------------------------------------------------------------------------------------------------

2) ping continu de pc1 vers un autre réseau (vers R2 par exemple) avec rupture 
de passerelle DS1: cette épreuve met en oeuvre la technologie HSRP

[root@pc1 ~]# ping 10.16.224.2   (connexion vers R2)
PING 10.16.224.2 (10.16.224.2) 56(84) bytes of data.
64 bytes from 10.16.224.2: icmp_seq=1 ttl=254 time=6.91 ms
64 bytes from 10.16.224.2: icmp_seq=2 ttl=254 time=6.17 ms
64 bytes from 10.16.224.2: icmp_seq=3 ttl=254 time=5.94 ms
64 bytes from 10.16.224.2: icmp_seq=4 ttl=254 time=5.74 ms
64 bytes from 10.16.224.2: icmp_seq=5 ttl=254 time=6.48 ms
64 bytes from 10.16.224.2: icmp_seq=6 ttl=254 time=7.00 ms
64 bytes from 10.16.224.2: icmp_seq=7 ttl=254 time=5.71 ms
64 bytes from 10.16.224.2: icmp_seq=8 ttl=254 time=5.22 ms
64 bytes from 10.16.224.2: icmp_seq=9 ttl=254 time=5.44 ms
64 bytes from 10.16.224.2: icmp_seq=10 ttl=254 time=6.63 ms
64 bytes from 10.16.224.2: icmp_seq=11 ttl=254 time=6.01 ms
64 bytes from 10.16.224.2: icmp_seq=12 ttl=254 time=6.22 ms
64 bytes from 10.16.224.2: icmp_seq=13 ttl=254 time=5.28 ms (rupture de passerelle DS1 avec des paquets perdus)
From 10.16.10.130 icmp_seq=21 Destination Host Unreachable
From 10.16.10.130 icmp_seq=22 Destination Host Unreachable
From 10.16.10.130 icmp_seq=23 Destination Host Unreachable
From 10.16.10.130 icmp_seq=24 Destination Host Unreachable
From 10.16.10.130 icmp_seq=25 Destination Host Unreachable
From 10.16.10.130 icmp_seq=26 Destination Host Unreachable
From 10.16.10.130 icmp_seq=27 Destination Host Unreachable
From 10.16.10.130 icmp_seq=28 Destination Host Unreachable
From 10.16.10.130 icmp_seq=29 Destination Host Unreachable
From 10.16.10.130 icmp_seq=30 Destination Host Unreachable
From 10.16.10.130 icmp_seq=31 Destination Host Unreachable
From 10.16.10.130 icmp_seq=32 Destination Host Unreachable
From 10.16.10.130 icmp_seq=33 Destination Host Unreachable
From 10.16.10.130 icmp_seq=34 Destination Host Unreachable
From 10.16.10.130 icmp_seq=35 Destination Host Unreachable
From 10.16.10.130 icmp_seq=36 Destination Host Unreachable
From 10.16.10.130 icmp_seq=37 Destination Host Unreachable
From 10.16.10.130 icmp_seq=38 Destination Host Unreachable
From 10.16.10.130 icmp_seq=39 Destination Host Unreachable
From 10.16.10.130 icmp_seq=40 Destination Host Unreachable
From 10.16.10.130 icmp_seq=41 Destination Host Unreachable
From 10.16.10.130 icmp_seq=42 Destination Host Unreachable
From 10.16.10.130 icmp_seq=43 Destination Host Unreachable
From 10.16.10.130 icmp_seq=44 Destination Host Unreachable
From 10.16.10.130 icmp_seq=45 Destination Host Unreachable
From 10.16.10.130 icmp_seq=46 Destination Host Unreachable
From 10.16.10.130 icmp_seq=47 Destination Host Unreachable
From 10.16.10.130 icmp_seq=48 Destination Host Unreachable
From 10.16.10.130 icmp_seq=49 Destination Host Unreachable
From 10.16.10.130 icmp_seq=50 Destination Host Unreachable
From 10.16.10.130 icmp_seq=51 Destination Host Unreachable
From 10.16.10.130 icmp_seq=52 Destination Host Unreachable
From 10.16.10.130 icmp_seq=53 Destination Host Unreachable
From 10.16.10.130 icmp_seq=54 Destination Host Unreachable
From 10.16.10.130 icmp_seq=55 Destination Host Unreachable
From 10.16.10.130 icmp_seq=56 Destination Host Unreachable
From 10.16.10.130 icmp_seq=57 Destination Host Unreachable
From 10.16.10.130 icmp_seq=58 Destination Host Unreachable
From 10.16.10.130 icmp_seq=59 Destination Host Unreachable
From 10.16.10.130 icmp_seq=60 Destination Host Unreachable
From 10.16.10.130 icmp_seq=61 Destination Host Unreachable
From 10.16.10.130 icmp_seq=62 Destination Host Unreachable
From 10.16.10.130 icmp_seq=63 Destination Host Unreachable
From 10.16.10.130 icmp_seq=64 Destination Host Unreachable
64 bytes from 10.16.224.2: icmp_seq=65 ttl=254 time=11.0 ms (Le DS2 intervient et prends le relais, HSRP est faible)
64 bytes from 10.16.224.2: icmp_seq=66 ttl=254 time=5.43 ms
64 bytes from 10.16.224.2: icmp_seq=67 ttl=254 time=5.88 ms
64 bytes from 10.16.224.2: icmp_seq=68 ttl=254 time=5.85 ms
64 bytes from 10.16.224.2: icmp_seq=69 ttl=254 time=4.46 ms
64 bytes from 10.16.224.2: icmp_seq=70 ttl=254 time=5.26 ms
64 bytes from 10.16.224.2: icmp_seq=71 ttl=254 time=4.88 ms
64 bytes from 10.16.224.2: icmp_seq=72 ttl=254 time=5.57 ms
64 bytes from 10.16.224.2: icmp_seq=73 ttl=254 time=5.27 ms
64 bytes from 10.16.224.2: icmp_seq=74 ttl=254 time=5.17 ms
64 bytes from 10.16.224.2: icmp_seq=75 ttl=254 time=5.83 ms

--- 10.16.224.2 ping statistics ---
75 packets transmitted, 24 received, +44 errors, 68% packet loss, time 74054ms
rtt min/avg/max/mdev = 4.461/5.979/11.050/1.218 ms, pipe 4

-----------------------------------------------------------------------------------------------------------
3) un ping continu d'un PC vers un PC d'un autre VLAN : de pc1 à pc2 (vlan 10 à vlan 20) avec rupture de la liaison Po1: fiabilité de STP d'un Vlan à un autre

[root@pc1 ~]# ping 10.16.20.1
PING 10.16.20.1 (10.16.20.1) 56(84) bytes of data.
64 bytes from 10.16.20.1: icmp_seq=1 ttl=63 time=8.27 ms
64 bytes from 10.16.20.1: icmp_seq=2 ttl=63 time=8.30 ms
64 bytes from 10.16.20.1: icmp_seq=3 ttl=63 time=7.88 ms
64 bytes from 10.16.20.1: icmp_seq=4 ttl=63 time=8.00 ms
64 bytes from 10.16.20.1: icmp_seq=5 ttl=63 time=7.92 ms
64 bytes from 10.16.20.1: icmp_seq=6 ttl=63 time=5.56 ms
64 bytes from 10.16.20.1: icmp_seq=7 ttl=63 time=8.66 ms
64 bytes from 10.16.20.1: icmp_seq=8 ttl=63 time=7.61 ms
64 bytes from 10.16.20.1: icmp_seq=9 ttl=63 time=7.05 ms
64 bytes from 10.16.20.1: icmp_seq=10 ttl=63 time=7.48 ms
64 bytes from 10.16.20.1: icmp_seq=11 ttl=63 time=8.30 ms
64 bytes from 10.16.20.1: icmp_seq=12 ttl=63 time=7.18 ms
64 bytes from 10.16.20.1: icmp_seq=13 ttl=63 time=9.13 ms  ! on désactive le po1 sur DS1 (paquets perdus)
From 10.16.10.130 icmp_seq=46 Destination Host Unreachable
From 10.16.10.130 icmp_seq=47 Destination Host Unreachable
From 10.16.10.130 icmp_seq=48 Destination Host Unreachable
From 10.16.10.130 icmp_seq=49 Destination Host Unreachable
From 10.16.10.130 icmp_seq=50 Destination Host Unreachable
From 10.16.10.130 icmp_seq=51 Destination Host Unreachable
From 10.16.10.130 icmp_seq=52 Destination Host Unreachable
From 10.16.10.130 icmp_seq=53 Destination Host Unreachable
From 10.16.10.130 icmp_seq=54 Destination Host Unreachable
From 10.16.10.130 icmp_seq=55 Destination Host Unreachable
From 10.16.10.130 icmp_seq=56 Destination Host Unreachable
From 10.16.10.130 icmp_seq=57 Destination Host Unreachable
From 10.16.10.130 icmp_seq=58 Destination Host Unreachable
From 10.16.10.130 icmp_seq=59 Destination Host Unreachable
From 10.16.10.130 icmp_seq=60 Destination Host Unreachable
From 10.16.10.130 icmp_seq=61 Destination Host Unreachable
64 bytes from 10.16.20.1: icmp_seq=62 ttl=63 time=1012 ms  ! Le DS2 prend le relais
64 bytes from 10.16.20.1: icmp_seq=63 ttl=63 time=13.1 ms
64 bytes from 10.16.20.1: icmp_seq=64 ttl=63 time=5.90 ms
64 bytes from 10.16.20.1: icmp_seq=65 ttl=63 time=8.22 ms
64 bytes from 10.16.20.1: icmp_seq=66 ttl=63 time=4.86 ms
64 bytes from 10.16.20.1: icmp_seq=67 ttl=63 time=6.24 ms
64 bytes from 10.16.20.1: icmp_seq=68 ttl=63 time=5.97 ms
64 bytes from 10.16.20.1: icmp_seq=69 ttl=63 time=5.49 ms
64 bytes from 10.16.20.1: icmp_seq=70 ttl=63 time=5.28 ms
64 bytes from 10.16.20.1: icmp_seq=71 ttl=63 time=7.21 ms
64 bytes from 10.16.20.1: icmp_seq=72 ttl=63 time=7.08 ms
64 bytes from 10.16.20.1: icmp_seq=73 ttl=63 time=5.80 ms
64 bytes from 10.16.20.1: icmp_seq=74 ttl=63 time=5.88 ms
64 bytes from 10.16.20.1: icmp_seq=75 ttl=63 time=6.23 ms
64 bytes from 10.16.20.1: icmp_seq=76 ttl=63 time=6.07 ms
64 bytes from 10.16.20.1: icmp_seq=77 ttl=63 time=5.37 ms
64 bytes from 10.16.20.1: icmp_seq=22 ttl=63 time=55823 ms
64 bytes from 10.16.20.1: icmp_seq=23 ttl=63 time=54825 ms
64 bytes from 10.16.20.1: icmp_seq=24 ttl=63 time=53826 ms
64 bytes from 10.16.20.1: icmp_seq=25 ttl=63 time=52828 ms
64 bytes from 10.16.20.1: icmp_seq=26 ttl=63 time=51830 ms
64 bytes from 10.16.20.1: icmp_seq=27 ttl=63 time=50831 ms
64 bytes from 10.16.20.1: icmp_seq=28 ttl=63 time=49839 ms
64 bytes from 10.16.20.1: icmp_seq=29 ttl=63 time=48842 ms
64 bytes from 10.16.20.1: icmp_seq=30 ttl=63 time=47843 ms
64 bytes from 10.16.20.1: icmp_seq=31 ttl=63 time=46845 ms
64 bytes from 10.16.20.1: icmp_seq=32 ttl=63 time=45846 ms
64 bytes from 10.16.20.1: icmp_seq=33 ttl=63 time=44849 ms
64 bytes from 10.16.20.1: icmp_seq=34 ttl=63 time=43850 ms
64 bytes from 10.16.20.1: icmp_seq=35 ttl=63 time=42851 ms
64 bytes from 10.16.20.1: icmp_seq=36 ttl=63 time=41851 ms
64 bytes from 10.16.20.1: icmp_seq=37 ttl=63 time=40852 ms
64 bytes from 10.16.20.1: icmp_seq=38 ttl=63 time=39883 ms
64 bytes from 10.16.20.1: icmp_seq=39 ttl=63 time=38906 ms
64 bytes from 10.16.20.1: icmp_seq=40 ttl=63 time=37921 ms
64 bytes from 10.16.20.1: icmp_seq=41 ttl=63 time=36970 ms
64 bytes from 10.16.20.1: icmp_seq=42 ttl=63 time=35990 ms
64 bytes from 10.16.20.1: icmp_seq=43 ttl=63 time=35015 ms
64 bytes from 10.16.20.1: icmp_seq=44 ttl=63 time=34017 ms
64 bytes from 10.16.20.1: icmp_seq=45 ttl=63 time=33019 ms
64 bytes from 10.16.20.1: icmp_seq=78 ttl=63 time=4.43 ms
64 bytes from 10.16.20.1: icmp_seq=79 ttl=63 time=5.57 ms
64 bytes from 10.16.20.1: icmp_seq=80 ttl=63 time=6.03 ms
64 bytes from 10.16.20.1: icmp_seq=81 ttl=63 time=6.29 ms
64 bytes from 10.16.20.1: icmp_seq=82 ttl=63 time=7.34 ms
64 bytes from 10.16.20.1: icmp_seq=83 ttl=63 time=8.83 ms
64 bytes from 10.16.20.1: icmp_seq=84 ttl=63 time=5.95 ms
64 bytes from 10.16.20.1: icmp_seq=85 ttl=63 time=5.96 ms
64 bytes from 10.16.20.1: icmp_seq=86 ttl=63 time=6.20 ms
64 bytes from 10.16.20.1: icmp_seq=87 ttl=63 time=6.61 ms
64 bytes from 10.16.20.1: icmp_seq=88 ttl=63 time=7.36 ms
64 bytes from 10.16.20.1: icmp_seq=89 ttl=63 time=5.82 ms
From 10.16.10.130 icmp_seq=103 Destination Host Unreachable ! On active le po1 (paquets perdus)
From 10.16.10.130 icmp_seq=104 Destination Host Unreachable
From 10.16.10.130 icmp_seq=105 Destination Host Unreachable
From 10.16.10.130 icmp_seq=106 Destination Host Unreachable
From 10.16.10.130 icmp_seq=107 Destination Host Unreachable
From 10.16.10.130 icmp_seq=108 Destination Host Unreachable
From 10.16.10.130 icmp_seq=109 Destination Host Unreachable
From 10.16.10.130 icmp_seq=110 Destination Host Unreachable
64 bytes from 10.16.20.1: icmp_seq=111 ttl=63 time=2020 ms  ! Le traffic est acheminé de nouveau vers DS1 
64 bytes from 10.16.20.1: icmp_seq=112 ttl=63 time=1021 ms
64 bytes from 10.16.20.1: icmp_seq=113 ttl=63 time=23.0 ms
64 bytes from 10.16.20.1: icmp_seq=114 ttl=63 time=8.96 ms
64 bytes from 10.16.20.1: icmp_seq=115 ttl=63 time=7.64 ms
64 bytes from 10.16.20.1: icmp_seq=116 ttl=63 time=7.66 ms
64 bytes from 10.16.20.1: icmp_seq=117 ttl=63 time=8.11 ms
64 bytes from 10.16.20.1: icmp_seq=118 ttl=63 time=7.41 ms
64 bytes from 10.16.20.1: icmp_seq=119 ttl=63 time=7.97 ms
64 bytes from 10.16.20.1: icmp_seq=120 ttl=63 time=8.99 ms
64 bytes from 10.16.20.1: icmp_seq=121 ttl=63 time=8.28 ms
64 bytes from 10.16.20.1: icmp_seq=122 ttl=63 time=7.49 ms
64 bytes from 10.16.20.1: icmp_seq=123 ttl=63 time=7.75 ms
64 bytes from 10.16.20.1: icmp_seq=124 ttl=63 time=8.30 ms
64 bytes from 10.16.20.1: icmp_seq=125 ttl=63 time=8.28 ms

--- 10.16.20.1 ping statistics ---
125 packets transmitted, 80 received, +24 errors, 36% packet loss, time 124090ms
rtt min/avg/max/mdev = 4.436/13370.198/55823.904/20648.839 ms, pipe 56




