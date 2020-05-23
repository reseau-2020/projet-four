%Configure IKE parameters

crypto isakmp policy 1
 encr des
 hash md5
 authentication pre-share
 group 5
 lifetime 86400
crypto isakmp key testtest address 192.168.122.33


% Configure IPSec parameters:

crypto ipsec transform-set to-fortigate-set esp-des esp-md5-hmac
!
!
!
crypto ipsec transform-set to-fortigate-set esp-aes 256 esp-sha-hmac
!
crypto map cm-to-fortigate 1 ipsec-isakmp
 set peer 192.168.122.33
 set transform-set to-fortigate-set
 match address crypto-acl
!
interface G0/1	
 crypto map cm-to-fortigate
!
!
no ip access-list extended lan
ip access-list extended lan
 5 deny ip 10.0.0.0 0.255.255.255 192.168.150.0 0.0.0.255
 10 permit ip 10.0.0.0 0.255.255.255 any

no ip access-list extended crypto-acl
ip access-list extended crypto-acl
 permit ip 192.168.150.0 0.0.0.255 10.0.0.0 0.255.255.255 
 permit ip 10.0.0.0 0.255.255.255 192.168.150.0 0.0.0.255
!
end
!
! ADAPTATION DU PARE-FEU
!
ip access-list extended ISAKMP_IPSEC
 permit udp any any eq isakmp
 permit ahp any any
 permit esp any any
 permit udp any any eq non500-isakmp
class-map type inspect match-any vpn-class
 match access-group name ISAKMP_IPSEC
policy-map type inspect to-self-policy
 class type inspect vpn-class
  inspect
end