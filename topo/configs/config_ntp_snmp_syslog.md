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

! Activation de Syslog

  	service timestamp log datetime
	service timestamp debug datetime
	 logging 10.32.202.3
	 logging facility local7
	 logging trap 1
	 logging trap 2
	 logging trap 3
	 logging trap 4
	 logging trap 5
	 logging trap 6
	 logging trap 7
	 logging origin-id hostname
	 exit
	wr

