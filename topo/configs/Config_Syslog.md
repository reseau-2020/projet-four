### Configuration du serveur syslog sur la machine Centos-7

! Installation du service syslog

````
yum -y install rsyslog
````
! Modification du dossier de configuaration : ( port TCP et décommenter la partie UDP et TCP syslog réception)
````
vi /etc/rsyslog.conf

# rsyslog configuration file
# For more information see /usr/share/doc/rsyslog-*/rsyslog_conf.html
# If you experience problems, see http://www.rsyslog.com/doc/troubleshoot.html
#### MODULES ####
# The imjournal module bellow is now used as a message source instead of imuxsocck.
$ModLoad imuxsock # provides support for local system logging (e.g. via logger ccommand)
$ModLoad imjournal # provides access to the systemd journal
#$ModLoad imklog # reads kernel messages (the same are read from journald)
#$ModLoad immark  # provides --MARK-- message capability
# Provides UDP syslog reception
$ModLoad imudp
$UDPServerRun 514
# Provides TCP syslog reception
$ModLoad imtcp
$InputTCPServerRun 1514
````

! Enregistrer les modifications et redémarrer le service syslog
````
systemctl restart rsyslog
````

### Configuration des postes de travail 

! installation du service rsyslog
````
yum -y install rsyslog
````

! Modification du dossier de configuaration
````
vi /etc/rsyslog.conf

### Per-Host Templates for Remote Systems ###
$template TmplAuthpriv, "/var/log/remote/auth/%HOSTNAME%/%PROGRAMNAME:::secpath--
replace%.log"
$template TmplMsg, "/var/log/remote/msg/%HOSTNAME%/%PROGRAMNAME:::secpath-replacc
e%.log"
# Provides UDP syslog reception
#$ModLoad imudp
#$UDPServerRun 514
# Provides TCP syslog reception
$ModLoad imtcp
# Adding this ruleset to process remote messages
$RuleSet remote1
authpriv.*   ?TmplAuthpriv
*.info;mail.none;authpriv.none;cron.none   ?TmplMsg
$RuleSet RSYSLOG_DefaultRuleset   #End the rule set by switching back to the deff
ault rule set
$InputTCPServerBindRuleset remote1  #Define a new input and bind it to the "remoo
te1" rule set
$InputTCPServerRun 10514
*.* @10.32.202.3:514
*.* @10.32.202.3:1514
````

! Enregistrer les modifications et redémarrer le service syslog
````
systemctl restart rsyslog
````

### Configuration des routeurs et switch
````
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
````
