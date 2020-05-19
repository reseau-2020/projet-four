# PLAN D'ADRESSAGE
Masque par défaut pour les adresses ipv4 : /24
Masque par défaut pour les adresses ipv6 : /64

| Périphérique  |Interfaces  |Infos  | Adresse ipv4  |  Adresse ipv6
|---|-----|-----|----|----|
R1 | Gi0/0 | connected to SW-R1 on port Ethernet0 | 10.32.1.1 | fe80::1 ; 
R1 | Gi0/1 | connected to Internet on port nat0   | 10.32.4.1 | fe80::1:cafe:4 ; 2001:470:c814:4001:: ; fd00:fd00:fd00:1::1
R1 | Gi0/2 | connected to R2 on port Gi0/1        | 10.32.2.1 | fe80::1
R1 | Gi0/3 | connected to R3 on port Gi0/1        | 10.32.3.1 | fe80::1
R1 | Gi0/7 | connected to SW-CTRL on port Ethernet1 | 10.32.5.1 | fe80::1
R2 | Gi0/0 | connected to SW-R2 on port Ethernet0   | 10.32.1.2 | fe80::2
R2 | Gi0/1 | connected to R1 on port Gi0/2  | 10.32.2.2 | fe80::2 ; 2001:470:c814:4002::1 ; fd00:fd00:fd00:2::1
R2 | Gi0/2 | connected to DS1 on port Gi2/0 | 10.16.1.2 | fe80::2 ; 2001:470:c814:4002::d1:1 ; fd00:fd00:fd00:2::d1:1
R2 | Gi0/3 | connected to R3 on port Gi0/2  | 10.32.3.2 | fe80::2 ; 2001:470:c814:4002::3 ; fd00:fd00:fd00:2::3
R2 | Gi0/4 | connected to DS1 on port Gi3/0 | 10.16.2.2 | fe80::2 ; 2001:470:c814:4002::d1:2 ; fd00:fd00:fd00:2::d1:2
R2 | Gi0/5 | connected to DS2 on port Gi2/1 | 10.16.3.2 | fe80::2 ; 2001:470:c814:4002::d2:1 ; fd00:fd00:fd00:2::d2:1
R2 | Gi0/6 | connected to DS2 on port Gi3/1 | 10.16.4.2 | fe80::2 ; 2001:470:c814:4002::d2:2 ; fd00:fd00:fd00:2::d2:2
R2 | Gi0/7 | connected to SW-CTRL on port Ethernet2 | 10.32.5.2 | fe80::2 ; 2001:470:c814:4002::c:1 ; fd00:fd00:fd00:2::c:1
R3 | Gi0/0 | connected to SW-R3 on port Ethernet0   | 10.32.0.3 | fe80::3 ; 
R3 | Gi0/1 | connected to R1 on port Gi0/3  | 10.32.1.3 | fe80::3 ; 2001:470:c814:4003::1 ; fd00:fd00:fd00:3::1
R3 | Gi0/2 | connected to R2 on port Gi0/3  | 10.32.2.3 | fe80::3 ; 2001:470:c814:4003::2 ; fd00:fd00:fd00:3::2
R3 | Gi0/3 | connected to DS2 on port Gi2/0 | 10.16.1.3 | fe80::3 ; 2001:470:c814:4003::d2:1 ; fd00:fd00:fd00:3::d2:1
R3 | Gi0/4 | connected to DS2 on port Gi3/0 | 10.16.2.3 | fe80::3 ; 2001:470:c814:4003::d2:2 ; fd00:fd00:fd00:3::d2:2
R3 | Gi0/5 | connected to DS1 on port Gi2/1 | 10.16.3.3 | fe80::3 ; 2001:470:c814:4003::d1:1 ; fd00:fd00:fd00:3::d1:1
R3 | Gi0/6 | connected to DS1 on port Gi3/1 | 10.16.4.3 | fe80::3 ; 2001:470:c814:4003::d1:2 ; fd00:fd00:fd00:3::d1:2
R3 | Gi0/7 | connected to SW-CTRL on port Ethernet3 | 10.32.5.3 | fe80::3
DS1 | Gi0/0 | connected to AS1 on port Gi0/0 | 10.16.7.11  | fe80::d:1 ; 2001:470:c814:4010::a1:1 ; fd00:fd00:fd00::10:a1:1
DS1 | Gi0/1 | connected to AS2 on port Gi0/1 | 10.16.9.11  | fe80::d:1 ; 2001:470:c814:4010::a2:1 ; fd00:fd00:fd00::10:a2:1
DS1 | Gi0/2 | connected to DS2 on port Gi0/2 | 10.16.11.11 | fe80::d:1 ; 2001:470:c814:4010::d2:1 ; fd00:fd00:fd00::10:d2:1
DS1 | Gi1/0 | connected to AS1 on port Gi1/0 | 10.16.8.11  | fe80::d:1 ; 2001:470:c814:4010::a1:2 ; fd00:fd00:fd00::10:a1:2
DS1 | Gi1/1 | connected to AS2 on port Gi1/1 | 10.16.10.11 | fe80::d:1 ; 2001:470:c814:4010::a2:2 ; fd00:fd00:fd00::10:a2:2
DS1 | Gi1/2 | connected to DS2 on port Gi1/2 | 10.16.12.11 | fe80::d:1 ; 2001:470:c814:4010::d2:2 ; fd00:fd00:fd00::10:d2:2
DS1 | Gi2/0 | connected to R2 on port Gi0/2  | 10.16.2.11  | fe80::d:1 ; 2001:470:c814:4010::20:1 ; fd00:fd00:fd00::10:20:1
DS1 | Gi2/1 | connected to R3 on port Gi0/5  | 10.16.3.11  | fe80::d:1 ; 2001:470:c814:4010::30:1 ; fd00:fd00:fd00::10:30:1
DS1 | Gi3/0 | connected to R2 on port Gi0/4  | 10.16.4.11  | fe80::d:1 ; 2001:470:c814:4010::20:2 ; fd00:fd00:fd00::10:20:2
DS1 | Gi3/1 | connected to R3 on port Gi0/6  | 10.16.6.11  | fe80::d:1 ; 2001:470:c814:4010::30:2 ; fd00:fd00:fd00::10:30:2
DS1 | Gi3/3 | connected to SW-CTRL on port Ethernet4 |10.16.5.11  | fe80::d:1 ; 2001:470:c814:4010:c:1 ; fd00:fd00:fd00:10:c:1
DS2 | Gi0/0 | connected to AS2 on port Gi0/0 | 10.16.8.12  | fe80::d:2 ; 2001:470:c814:4020::a2:1 ; fd00:fd00:fd00:20::a2:1
DS2 | Gi0/1 | connected to AS1 on port Gi0/1 | 10.16.7.12  | fe80::d:2 ; 2001:470:c814:4020::a1:1 ; fd00:fd00:fd00:20::a1:1
DS2 | Gi0/2 | connected to DS1 on port Gi0/2 | 10.16.10.12 | fe80::d:2 ; 2001:470:c814:4020::d1:1 ; fd00:fd00:fd00:20::d1:1
DS2 | Gi1/0 | connected to AS2 on port Gi1/0 | 10.16.9.12  | fe80::d:2 ; 2001:470:c814:4020::a2:2 ; fd00:fd00:fd00:20::a2:2
DS2 | Gi1/1 | connected to AS1 on port Gi1/1 | 10.16.8.12  | fe80::d:2 ; 2001:470:c814:4020::a1:2 ; fd00:fd00:fd00:20::a1:2
DS2 | Gi1/2 | connected to DS1 on port Gi1/2 | 10.16.11.12 | fe80::d:2 ; 2001:470:c814:4020::d1:2 ; fd00:fd00:fd00:20::d1:2
DS2 | Gi2/0 | connected to R3 on port Gi0/3 | 10.16.3.12   | fe80::d:2 ; 2001:470:c814:4020::30:1 ; fd00:fd00:fd00:20::30:1
DS2 | Gi2/1 | connected to R2 on port Gi0/5 | 10.16.2.12   | fe80::d:2 ; 2001:470:c814:4020::20:1 ; fd00:fd00:fd00:20::20:1
DS2 | Gi3/0 | connected to R3 on port Gi0/4 | 10.16.6.12   | fe80::d:2 ; 2001:470:c814:4020::30:2 ; fd00:fd00:fd00:20::30:2
DS2 | Gi3/1 | connected to R2 on port Gi0/6 | 10.16.4.12   | fe80::d:2 ; 2001:470:c814:4020::20:2 ; fd00:fd00:fd00:20::20:2
DS2 | Gi3/3 | connected to SW-CTRL on port Ethernet5 | 10.16.5.12 |fe80::d:2 ; 2001:470:c814:4020::c:1 ; fd00:fd00:fd00:10::c:2
AS1 |  Gi0/0 | connected to DS1 on port Gi0/0 | 10.16.1.13 | fe80::a:1 ; 2001:470:c814:4100::d1:1 ; fd00:fd00:fd00:100::d1:1
AS1 |  Gi0/1 | connected to DS2 on port Gi0/1 | 10.16.2.13 | fe80::a:1 ; 2001:470:c814:4100::d2:1 ; fd00:fd00:fd00:100::d2:1
AS1 |  Gi1/0 | connected to DS1 on port Gi1/0 | 10.16.3.13 | fe80::a:1 ; 2001:470:c814:4100::d1:2 ; fd00:fd00:fd00:100::d1:2
AS1 |  Gi1/1 | connected to DS2 on port Gi1/1 | 10.16.4.13 | fe80::a:1 ; 2001:470:c814:4100::d2:2 ; fd00:fd00:fd00:100::d2:2
AS1 |  Gi2/0 | connected to pc-1 on port eth0 | 10.16.6.13 | fe80::a:1 ; 2001:470:c814:4100::ff:1 ; fd00:fd00:fd00:100::ff:1
AS1 |  Gi2/1 | connected to pc-2 on port eth0 | 10.16.7.13 | fe80::a:1 ; 2001:470:c814:4100::ff:2 ; fd00:fd00:fd00:100::ff:2
AS1 |  Gi2/2 | connected to pc-3 on port eth0 | 10.16.8.13 | fe80::a:1 ; 2001:470:c814:4100::ff:3 ; fd00:fd00:fd00:100::ff:3
AS1 |  Gi2/3 | connected to pc-4 on port eth0 | 10.16.9.13 | fe80::a:1 ; 2001:470:c814:4100::ff:4 ; fd00:fd00:fd00:100::ff:4
AS1 |  Gi3/3 | connected to SW-CTRL on port Ethernet6 | 10.16.5.13 | fe80::a:1 ; 2001:470:c814:4100::c:1 ; fd00:fd00:fd00:100::c:1
AS2 | Gi0/0 | connected to DS2 on port Gi0/0 | 10.16.1.14 | fe80::a:2 ; 2001:470:c814:4200::d2:1 ; fd00:fd00:fd00:200::d2:1
AS2 | Gi0/1 | connected to DS1 on port Gi0/1 | 10.16.2.14 | fe80::a:2 ; 2001:470:c814:4200::d1:1 ; fd00:fd00:fd00:200::d1:1
AS2 | Gi1/0 | connected to DS2 on port Gi1/0 | 10.16.3.14 | fe80::a:2 ; 2001:470:c814:4200::d2:2 ; fd00:fd00:fd00:200::d2:2
AS2 | Gi1/1 | connected to DS1 on port Gi1/1 | 10.16.4.14 | fe80::a:2 ; 2001:470:c814:4200::d1:2 ; fd00:fd00:fd00:200::d1:2
AS2 | Gi2/0 | connected to pc-5 on port eth0 | 10.16.6.14 | fe80::a:2 ; 2001:470:c814:4200::ff:5 ; fd00:fd00:fd00:200::ff:5
AS2 | Gi2/1 | connected to pc-6 on port eth0 | 10.16.7.14 | fe80::a:2 ; 2001:470:c814:4200::ff:6 ; fd00:fd00:fd00:200::ff:6
AS2 | Gi2/2 | connected to pc-7 on port eth0 | 10.16.8.14 | fe80::a:2 ; 2001:470:c814:4200::ff:7 ; fd00:fd00:fd00:200::ff:7
AS2 | Gi2/3 | connected to pc-8 on port eth0 | 10.16.9.14 | fe80::a:2 ; 2001:470:c814:4200::ff:8 ; fd00:fd00:fd00:200::ff:8
AS2 | Gi3/3 | connected to SW-CTRL on port Ethernet7 | 10.16.5.14 | fe80::a:2 ; 2001:470:c814:4200::c:1 ; fd00:fd00:fd00:200::c:1
SW-CTRL | Port Ethernet0 is in access  mode, connected to controller-1 on port Ethernet0 |  | fe80::c:1
SW-CTRL | Port Ethernet1 is in access  mode, connected to R1 on port Gi0/7 |  | fe80::c:1
SW-CTRL | Port Ethernet2 is in access  mode, connected to R2 on port Gi0/7 |  | fe80::c:1
SW-CTRL | Port Ethernet3 is in access  mode, connected to R3 on port Gi0/7 |  | fe80::c:1
SW-CTRL | Port Ethernet4 is in access  mode, connected to DS1 on port Gi3/3 |  | fe80::c:1
SW-CTRL | Port Ethernet5 is in access  mode, connected to DS2 on port Gi3/3 |  | fe80::c:1
SW-CTRL | Port Ethernet6 is in access  mode, connected to AS1 on port Gi3/3 |  | fe80::c:1
SW-CTRL | Port Ethernet7 is in access  mode, connected to AS2 on port Gi3/3 |  | fe80::c:1


# VLANS
- vlan 10 : 10.16.10.0/24, ip default gateway 10.16.10.254
- vlan 20 : 10.16.20.0/24, passerelle 10.16.10.254
- vlan 30 : 10.16.30.0/24, passerelle 10.16.10.254
- vlan 40 : 10.16.40.0/24, passerelle 10.16.10.254
- vlan 99 : vlan natif

| Périphérique  |VLAN | Adresse ipv4  |  Adresse ipv6
|---|-----|----|----|
DS1 | VLAN10 | 10.16.10.252/24 | fd00:abc:10::1/24 ; 2001:470:c814:4010::1/64
DS1 | VLAN20 | 10.16.20.252/24 | fd00:abc:20::1/24 ; 2001:470:c814:4020::1/64 
DS1 | VLAN30 | 10.16.30.252/24 | fd00:abc:30::1/24 ; 2001:470:c814:4030::1/64
DS1 | VLAN40 | 10.16.40.252/24 | fd00:abc:40::1/24 ; 2001:470:c814:4040::1/64
DS2 | VLAN10 | 10.16.10.253/24 | fd00:abc:10::2/24 ; 2001:470:c814:4010::2/64
DS2 | VLAN20 | 10.16.20.253/24 | fd00:abc:20::2/24 ; 2001:470:c814:4020::2/64
DS2 | VLAN30 | 10.16.30.253/24 | fd00:abc:30::2/24 ; 2001:470:c814:4030::2/64
DS2 | VLAN40 | 10.16.40.253/24 | fd00:abc:40::2/24 ; 2001:470:c814:4040::2/64
