```
!
! PARE-FEU
!
conf t
 class-map type inspect match-any internet-trafic-class
  match protocol http
  match protocol https
  match protocol dns
  match protocol icmp
  match protocol ssh
end
!
conf t
 policy-map type inspect internet-trafic-policy
  class type inspect internet-trafic-class
   inspect
end
!
conf t
zone security lan
zone security internet
interface G0/1
 zone-member security internet
interface G0/2
 zone-member security lan
interface G0/3
 zone-member security lan
end
!
conf t
zone-pair security lan-internet source lan destination internet
  service-policy type inspect internet-trafic-policy
end
!
! DMZ
!
conf t
class-map type inspect match-any lan-dmz-class
 match protocol http
 match protocol https
 match protocol ssh
policy-map type inspect lan-dmz-policy
 class type inspect lan-dmz-class
 inspect
zone security dmz
interface g0/0
 zone-member security dmz
zone-pair security lan-dmz source lan destination dmz
 service-policy type inspect lan-dmz-policy
end
!
conf t
interface G0/0
 zone security dmz
class-map type inspect match-any internet-dmz-class
 match protocol http
 match protocol https
policy-map type inspect internet-dmz-policy
 class type inspect internet-dmz-class
 inspect
zone-pair security internet-dmz source internet destination dmz
 service-policy type inspect internet-dmz-policy
end
!
! Transport de port
!
conf t
ip nat inside source static tcp 10.32.201.2 80 interface G0/1 80
!
ip nat inside source static tcp 10.32.201.2 443 interface G0/1 443
end
!
conf t
zone-pair security dmz-internet source dmz destination internet
 service-policy type inspect internet-trafic-policy
end
!
! MISE EN PLACE
!
conf t
ip access-list extended SSH
 permit tcp any any eq 22
 deny tcp any any
class-map type inspect match-any remote-access-class
 match access-group name SSH
class-map type inspect match-any icmp-class
 match protocol icmp
policy-map type inspect to-self-policy
 class type inspect remote-access-class
  pass
 class type inspect icmp-class
  inspect
 class class-default
  drop log
zone-pair security internet-self source internet destination self
 service-policy type inspect to-self-policy
end
!
! ACCESS-LIST DE GESTION
!
!conf t
!ip access-list standard SSH_ACCESS
! permit ...
! permit ...
! deny   any
!line vty 0 4
! access-class SSH_ACCESS in
!
! DHCP
!
conf t
ip access-list extended DHCP
 permit udp any eq 67 any eq 68
 permit udp any eq 68 any eq 67
class-map type inspect match-any dhcp-class
 match access-group name DHCP
policy-map type inspect to-self-policy
 class type inspect dhcp-class
  pass
end
!
! DNS
!
conf t
ip access-list extended DNS
 permit udp any any eq 53
 permit udp any eq 53 any
 deny udp any any
class-map type inspect match-any dns-class
 match access-group name DNS
policy-map type inspect to-self-policy
 class type inspect dns-class
  pass
end
```
