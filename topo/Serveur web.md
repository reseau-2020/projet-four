### Configuration d'un serveur web apache2 sur le server de la DMZ du réseau Remote (Fortigate)


## Configuration du serveur web Ubuntu

# Adressage IPv4 avec netplan

	vi /etc/netplan/*.yaml

	network:
	  version: 2
	  renderer: networkd
	  ethernets:
	    eth0:
	      addresses: [192.168.10.1/24]
	      gateway4: 192.168.10.254
	      nameservers:
	              addresses: [1.1.1.1, 8.8.8.8]
	      dhcp4: false
	      dhcp6: false

% Appliquer les nouveaux réglages et redémarrer networkd

netplan apply
systemctl restart systemd-networkd

# Installer un serveur apache2, mysql, php

	apt install apache2 php libapache2-mod-php mysql-server php-mysql
	apt install net-tools

	% Démarre le service web apache2
	netstat -antp | grep apache2


## Configuration Virtual IP sur Fortigate pour rediriger traffic http entrant de 192.168.122.29:80 vers 192.168.10.1:80 Idem pour HTTPS

Référence: [Fortinet Library](https://docs.fortinet.com/document/fortigate/5.4.0/cookbook/361386 "cliquez ici !")

# 1 Configuring the FortiGate's DMZ interface

Go to Network > Interfaces and edit the DMZ interface.
This example uses the port3 interface as the DMZ interface. The interface Alias indicates that this is the DMZ interface. As well the Role is set to DMZ.
For enhanced security, disable all Administrative Access options.


# 2 Creating virtual IPs

Go to Policy & Objects > Virtual IPs. Create two virtual IPs: one for HTTP access and one for HTTPS access.
Each virtual IP has the same address, mapping from the Internet to the DMZ interface. The difference is the port for each traffic type: port 80 for HTTP and port 443 for HTTPS.

# 3 Creating firewall policies

Go to Policy & Objects > Virtual IPs. Create two virtual IPs: one for HTTP access and one for HTTPS access.
Each virtual IP has the same address, mapping from the Internet to the DMZ interface. The difference is the port for each traffic type: port 80 for HTTP and port 443 for HTTPS.
Create a second firewall policy to allow HTTP and HTTPS traffic from the internal network to the web server.
Do not enable NAT. If you enable source NAT the configuration will still work but all traffic received by the web server will have the same source IP address so you will loose information about your website users.
You can also enable logging for all sessions to make it easier to test the configuration.

# 4 Results

Internet users and internal network users can access the web server by browsing to the web server's Internet address (in this example, http://172.20.120.35 and https://172.20.120.35). Internal users can also access the web server using its DMZ address (in this example, http://10.10.10.22 and https://10.10.10.22).
Since only HTTP and HTTPS are enabled, the web server is not accessible using other protocols (such as FTP) and you also cannot ping the web server from the Internet or from the internal network.
Go to FortiView Policies to see current sessions for each firewall policy. If you add a filter to just show policies with the DMZ interface as the destination interface you will see sessions from the Internal network to the web server and from the Internet to the web server.
Double-clicking on the Internet to DMZ web server session shows sessions from Internet addresses (in the example 172.20.120.100) and from the internal network (192.1681.20).


Test: [serveur web](http://192.168.122.29 "cliquez ici !")
