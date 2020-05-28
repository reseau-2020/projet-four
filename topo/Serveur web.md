## Configuration d'un serveur web apache2 sur le server de la DMZ du réseau Remote (Fortigate)

### Configuration du serveur web Ubuntu

Sur le serveur web nous devons d'abord paramétrer une adresse IP fixe cohérente avec le bloque IPv4 choisit pour le réseau de la DMZ : 192.168.10.0/24. Sur Ubuntu nous faisons les modifications d'adressage avec "Netplan": 

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
    # Appliquer les nouveaux réglages et redémarrer networkd
    netplan apply
    systemctl restart systemd-networkd

Nous devons ensuite installer un serveur HTTP sur la machine. Nous utiliserons apache2 pour la simplicitée avec php et mysql.

    apt install apache2 php libapache2-mod-php mysql-server php-mysql
    apt install net-tools
	
    # Démarre le service web apache2
    systemctl restart apache2.service
    # vérifier que le service apache2 est bien sur écoute du port 80
    netstat -antp | grep apache2

### Configuration Virtual IP sur Fortigate pour rediriger traffic http entrant de 192.168.122.29:80 vers 192.168.10.1:80 Idem pour HTTPS

Pour accéder aux pages web présente sur le serveur de la DMZ depuis l'extérieur (WAN) le traffic HTTP arrivant sur le port 3 (192.168.122.29) du parfeu Fortigate (qui fait aussi office de routeur ici) devra être redirigé vers l'adresse 192.168.10.1 sur le port 80.

On utilise une procédure mise à disposition sur le site de Fortrinet

Référence: [Fortinet Library](https://docs.fortinet.com/document/fortigate/5.4.0/cookbook/361386 "cliquez ici !")

1. Configuring the FortiGate's DMZ interface:

Go to **Network > Interfaces** and edit the DMZ interface.
This example uses the port3 interface as the DMZ interface. The interface Alias indicates that this is the DMZ interface. As well the Role is set to DMZ.
For enhanced security, disable all Administrative Access options.

2. Creating virtual IPs:

Go to **Policy & Objects > Virtual IPs.** Create two virtual IPs: one for HTTP access and one for HTTPS access.
Each virtual IP has the same address, mapping from the Internet to the DMZ interface. The difference is the port for each traffic type: port 80 for HTTP and port 443 for HTTPS.

3. Creating firewall policies:

Go to **Policy & Objects > IPv4 Policy.** Create a firewall policy to allow HTTP and HTTPS traffic from the Internet to the web server. Add both VIPs as the destination address.
Do not enable NAT. Enabling the NAT option actually enables source NAT which is not required for this configuration since the VIPs are added to perform destination NAT. If you do enable source NAT the configuration will still work but all traffic received by the web server will have the same source IP address so you will loose information about your website users.
You can also enable logging for all sessions to make it easier to test the configuration.
Create a second firewall policy to allow HTTP and HTTPS traffic from the internal network to the web server.

4. Results

Internet users and internal network users can access the web server by browsing to the web server's Internet address  http://192.168.122.29. Internal users can also access the web server using its DMZ address (in this example, http://192.168.10.1.
Since only HTTP and HTTPS are enabled, the web server is not accessible using other protocols (such as FTP) and you also cannot ping the web server from the Internet or from the internal network.
Go to FortiView Policies to see current sessions for each firewall policy. If you add a filter to just show policies with the DMZ interface as the destination interface you will see sessions from the Internal network to the web server and from the Internet to the web server.
Double-clicking on the Internet to DMZ web server session shows sessions from Internet addresses and from the internal network.

Test: [serveur web](http://192.168.122.29 "cliquez ici !")
