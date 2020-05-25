

! VPN IPSEC
```
crypto isakmp policy 1
 encr aes 256
 authentication pre-share
 group 5
 lifetime 7200
 
crypto isakmp key testtest address 192.168.122.33

crypto ipsec transform-set to-fortigate-set esp-aes 256 esp-sha-hmac

crypto map cm-to-fortigate 1 ipsec-isakmp
 set peer 192.168.122.33
 set transform-set to-fortigate-set
 match address crypto-acl

interface G0/1	
 crypto map cm-to-fortigate

ip access-list extended crypto-acl
 permit ip 10.32.0.0 0.255.255.255 192.168.122.0 0.0.0.255

no ip access-list standard lan
ip access-list extended lan
 5 deny ip 10.32.0.0 0.0.255.255 192.168.122.0 0.0.0.255
 10 permit ip 10.32.0.0 0.255.255.255 any

end
```
! ADAPTATION DU PARE-FEU
```
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
```
