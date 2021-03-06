````
! Connectivité en IPV4

! Exemples de test de connectivité dans la topologie de base (en interne et vers l'internet)

- De R3 à R1:
R3#ping 10.32.13.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.32.13.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 2/2/3 ms

- de DS2 à R2 (interface g0/5):
DS2#ping 10.16.215.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.16.215.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 2/2/3 ms

- de DS2 à R2 (interface g0/6)
DS2#ping 10.16.225.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.16.225.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 2/2/2 ms

- De pc5 à R3
[root@pc5 ~]# ping 10.16.135.1
PING 10.16.135.1 (10.16.135.1) 56(84) bytes of data.
64 bytes from 10.16.135.1: icmp_seq=1 ttl=254 time=6.31 ms
64 bytes from 10.16.135.1: icmp_seq=2 ttl=254 time=8.21 ms
64 bytes from 10.16.135.1: icmp_seq=3 ttl=254 time=7.14 ms
64 bytes from 10.16.135.1: icmp_seq=4 ttl=254 time=5.87 ms

--- 10.16.135.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 5.872/6.887/8.215/0.897 ms

- De pc8 à pc1: (de vlan40 à vlan 10)
[root@pc8 ~]# ping 10.16.10.1
PING 10.16.10.1 (10.16.10.1) 56(84) bytes of data.
64 bytes from 10.16.10.1: icmp_seq=1 ttl=63 time=9.51 ms
64 bytes from 10.16.10.1: icmp_seq=2 ttl=63 time=9.39 ms
64 bytes from 10.16.10.1: icmp_seq=3 ttl=63 time=10.1 ms
64 bytes from 10.16.10.1: icmp_seq=4 ttl=63 time=7.95 ms
64 bytes from 10.16.10.1: icmp_seq=5 ttl=63 time=8.32 ms

--- 10.16.10.1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4006ms
rtt min/avg/max/mdev = 7.958/9.059/10.108/0.802 ms

- De pc1 à pc5 (dans le même vlan10)
[root@pc1 ~]# ping 10.16.10.2
PING 10.16.10.2 (10.16.10.2) 56(84) bytes of data.
64 bytes from 10.16.10.2: icmp_seq=1 ttl=64 time=11.9 ms
64 bytes from 10.16.10.2: icmp_seq=2 ttl=64 time=7.32 ms
64 bytes from 10.16.10.2: icmp_seq=3 ttl=64 time=7.17 ms

--- 10.16.10.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 7.174/8.827/11.987/2.237 ms

- De DS2 à l'internet
DS2#ping 1.1.1.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.1.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 5/5/7 ms

  - de pc1 à l'internet:
[root@pc1 ~]# ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=56 time=9.81 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=56 time=9.53 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=56 time=9.69 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=56 time=9.06 ms
64 bytes from 1.1.1.1: icmp_seq=5 ttl=56 time=15.4 ms
64 bytes from 1.1.1.1: icmp_seq=6 ttl=56 time=9.59 ms
64 bytes from 1.1.1.1: icmp_seq=7 ttl=56 time=10.7 ms

--- 1.1.1.1 ping statistics ---
7 packets transmitted, 7 received, 0% packet loss, time 6009ms
rtt min/avg/max/mdev = 9.060/10.562/15.493/2.068 ms

- de pc3 à l'internet
[root@pc3 ~]# ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=56 time=10.8 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=56 time=11.4 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=56 time=10.1 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=56 time=9.15 ms

--- 1.1.1.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 9.157/10.389/11.448/0.863 ms

- de pc6 à l'internet:
[root@pc6 ~]# ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=56 time=10.7 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=56 time=13.9 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=56 time=9.95 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=56 time=10.0 ms

--- 1.1.1.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 9.956/11.191/13.985/1.643 ms

- de pc8 à l'internet:
[root@pc8 ~]# ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=56 time=10.3 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=56 time=8.54 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=56 time=9.31 ms

--- 1.1.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 8.546/9.409/10.364/0.753 ms

- De centos8-1 à l'internet
[root@pc1-r1 ~]# ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=58 time=4.77 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=58 time=3.77 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=58 time=3.91 ms

--- 1.1.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 5ms
rtt min/avg/max/mdev = 3.765/4.148/4.772/0.447 ms

- de centos8-2 à R1:
[root@pc2-r2 ~]# ping 10.32.201.1
PING 10.32.201.1 (10.32.201.1) 56(84) bytes of data.
64 bytes from 10.32.201.1: icmp_seq=1 ttl=255 time=2.01 ms
64 bytes from 10.32.201.1: icmp_seq=2 ttl=255 time=1.95 ms
64 bytes from 10.32.201.1: icmp_seq=3 ttl=255 time=1.76 ms
64 bytes from 10.32.201.1: icmp_seq=4 ttl=255 time=1.97 ms
64 bytes from 10.32.201.1: icmp_seq=5 ttl=255 time=1.82 ms
64 bytes from 10.32.201.1: icmp_seq=6 ttl=255 time=1.53 ms

--- 10.32.201.1 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 13ms
rtt min/avg/max/mdev = 1.528/1.838/2.009/0.171 ms



! Exemples de test de connectivité dans le site Fortigate et vers le site cisco

- De centos-1 au fortios-1
[root@pc1-fortinet ~]# ping 192.168.150.254
PING 192.168.150.254 (192.168.150.254) 56(84) bytes of data.
64 bytes from 192.168.150.254: icmp_seq=1 ttl=255 time=1.15 ms
64 bytes from 192.168.150.254: icmp_seq=2 ttl=255 time=0.889 ms
64 bytes from 192.168.150.254: icmp_seq=3 ttl=255 time=1.15 ms

--- 192.168.150.254 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 0.889/1.066/1.157/0.131 ms

- De centos-1 à l'internet
[root@pc1-fortinet ~]# ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=58 time=4.23 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=58 time=3.92 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=58 time=3.65 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=58 time=3.96 ms
64 bytes from 1.1.1.1: icmp_seq=5 ttl=58 time=3.97 ms

--- 1.1.1.1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4006ms
rtt min/avg/max/mdev = 3.653/3.948/4.233/0.188 ms

- De Centos-1 au pc1 se site cisco
[root@pc1-fortinet ~]# ping 10.16.10.2
PING 10.16.10.2 (10.16.10.2) 56(84) bytes of data.
64 bytes from 10.16.10.2: icmp_seq=1 ttl=60 time=12.7 ms
64 bytes from 10.16.10.2: icmp_seq=2 ttl=60 time=9.07 ms
64 bytes from 10.16.10.2: icmp_seq=3 ttl=60 time=9.63 ms
64 bytes from 10.16.10.2: icmp_seq=4 ttl=60 time=9.90 ms
64 bytes from 10.16.10.2: icmp_seq=5 ttl=60 time=9.30 ms

--- 10.16.10.2 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4006ms
rtt min/avg/max/mdev = 9.075/10.144/12.798/1.362 ms


! Exemples de test de connectivité au site distant (via le tunnel VPN):

- De R2 au fortios-1
R2#ping 192.168.122.27
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.122.27, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 2/3/6 ms

- de R2 au centos-1 de site fortigate
R2#ping 192.168.150.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.150.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/3/7 ms


- De pc5 au fortios-1
[root@pc5 ~]# ping 192.168.122.27
PING 192.168.122.27 (192.168.122.27) 56(84) bytes of data.
64 bytes from 192.168.122.27: icmp_seq=1 ttl=252 time=8.03 ms
64 bytes from 192.168.122.27: icmp_seq=2 ttl=252 time=6.98 ms
64 bytes from 192.168.122.27: icmp_seq=3 ttl=252 time=7.21 ms
64 bytes from 192.168.122.27: icmp_seq=4 ttl=252 time=7.86 ms
64 bytes from 192.168.122.27: icmp_seq=5 ttl=252 time=7.28 ms
64 bytes from 192.168.122.27: icmp_seq=6 ttl=252 time=7.32 ms

--- 192.168.122.27 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5006ms
rtt min/avg/max/mdev = 6.980/7.449/8.030/0.377 ms

-De pc1 au fortios-1 (via le tunnel vpn)
[root@pc1 ~]# ping 192.168.122.27
PING 192.168.122.27 (192.168.122.27) 56(84) bytes of data.
64 bytes from 192.168.122.27: icmp_seq=1 ttl=252 time=11.3 ms
64 bytes from 192.168.122.27: icmp_seq=2 ttl=252 time=7.36 ms
64 bytes from 192.168.122.27: icmp_seq=3 ttl=252 time=7.95 ms
64 bytes from 192.168.122.27: icmp_seq=4 ttl=252 time=6.79 ms
64 bytes from 192.168.122.27: icmp_seq=5 ttl=252 time=7.72 ms

--- 192.168.122.27 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4007ms
rtt min/avg/max/mdev = 6.797/8.244/11.380/1.619 ms

- De pc1 au centos-1 de site fortigate (connexion en ssh)
[root@pc1 ~]# ssh 192.168.150.1
root@192.168.150.1's password:
Last login: Tue May 26 11:34:27 2020 from 10.16.10.1
[root@pc1-fortinet ~]#

- De pc6 au centos-1 de site fortigate (connexion en ssh)
[root@pc6 ~]# ssh 192.168.150.1
The authenticity of host '192.168.150.1 (192.168.150.1)' can't be established.
ECDSA key fingerprint is SHA256:kg1ntg5jCx/MO3JNcV/Snj4IdSzRzL6RcbbiErQm0wk.
ECDSA key fingerprint is MD5:c3:30:dc:82:37:4b:49:5c:c3:b5:7e:18:65:5e:2b:66.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.150.1' (ECDSA) to the list of known hosts.
root@192.168.150.1's password:
Last login: Tue May 26 11:38:30 2020 from 10.16.10.1
[root@pc1-fortinet ~]#

- De pc4 au fortios-1 (connexion comme admin en ssh)
[root@pc4 ~]# ssh admin@192.168.122.27
WARNING: File System Check Recommended! Unsafe reboot may have caused inconsistency in disk drive.
It is strongly recommended that you check file system consistency before proceeding.
Please run 'execute disk scan 17'
Note: The device will reboot and scan during startup. This may take up to an hour
Firewall-groupe4 #  ! Accès au parefeu Fortios-1

! La connexion ssh via le tunnel VPN n'a pas pu être montée de site fortigate au site cisco. 

````















  

