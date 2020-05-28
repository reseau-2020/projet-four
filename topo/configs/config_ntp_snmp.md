! Configuration ntp:

	Conf t
	ntp server 3.fr.pool.ntp.org
	ntp update-calendar

! Vérification:

	show calendar
	Show clock
	Show ntp config
	exit

! Activation de la communauté snmp:

	conf t
	snmp-server community private RO

	! Activation des traps:
	snmp-server enable traps
	
	! choix de la destination et la communauté snmp:
	snmp-server host 10.32.202.3 private       !10.32.201.3 est l’adresse du serveur snmp
	exit
	! Enregistrement
	copy running-config startup-config
	
! Vérification:

	Show snmp community

