! Configuration de base FortiOS

	! Entrer en mode configuration globale
	configuration system interface

	! Paramétrage IPv4 de l'interface côté lan
	edit port2		
	 set mode static			
	 set ip 192.168.50.254 255.255.255.0
	 append allowaccess http		! ajout accès à Fortigate via http

	! Paramétrage IPv4 de l'interface côté wan
	edit port3
	 set mode dhcp
	 append allowaccess http	! ajout accès à Fortigate via http

	! Paramétrage IPv4 de l'interface côté DMZ
	edit port4		
	 set mode static			
	 set ip 192.168.10.254 255.255.255.0

	 ! pour obtenir l'adresse IPv4 du port3
	 get system interface physical
