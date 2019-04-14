# EdgeAutoDocumentation
This is the documentation for the Virtual Machine portion of the project EdgeAuto.

# VM setup on Google Cloud

Go to console.cloud.google.com and login. Navigate to the compute engine.

### Firewall Rules

Navigate to VPC Network and select Firewall Rules

We are creating 2 Firewall Rules.
One for incoming connections and one for outgoing.

#### Incoming Firewall Rule:
1. Name it something memorable, we used TCPIN
2. Direction of traffic: Ingress
3. Target Tags: edgeauto
4. Source IP Ranges: 0.0.0.0/0 This is used for all ranges.
5. Protocols and Ports: Allow all or the specific ports you are using. Check TCP and put the port you want to use. We used 8001.

#### Outgoing Firewall Rule:
1. Incoming: Name it something memorable, we used TCPIN
2. Direction of traffic: Ingress
3. Target Tags: edgeauto
4. Source IP Ranges: 0.0.0.0/0
5. Protocols and Ports: Allow all or the specific ports you are using. Check TCP and put the port you want to use. We used 8002.



### Nodes
On the left Click Instance Templates

1. Name your Instance: We used the scheme edgeauto-#
2. Select  machine type: 1vCPU with 3.75GB of memory
3. Select Boot Disk: Ubuntu 16.04 LTS
4. Allow HTTP Traffic and HTTPS Traffic
5. Select Networking and give the template a Network Tag. We used edgeauto.

Create the template. Now when you want to create a node you can use that template.
### Data Center
1. For our DataCenter:
2. Machine Type: 2vCPUs
3. Boot Disk: Ubuntu 16.04 LTS
4. Allow HTTP/HTTPS Traffic
5. Add a your Network Tag. Ours was edgeauto.

Create the VM

# Initial Setup on VMs
Pull from my github

`git clone https://github.com/SirAlfy/EdgeAutoDocs.git`

Navigate to that folder

`cd EdgeAutoDocs`

Run the bash file to start installing the dependencies

`sh edgeautoSetup.sh`

After installation you are able to run the socket. I would recommend doing this in a screen

`Screen -S PhpSocket`

followed by running the socket.

`php serverSocket.php`

To send the data to our Datacenter run the following command to execute it once

`php writeToNas.php`

or you can schedule it by editing your crontab

`sudo crontab -e`

Then put the following in with the following format

`Minute(0-59) Hour(0-23) Day(1-31) Month(1-12) Day of Week (0-6)(0=Sunday) /path/to/yourShellScript`

This code will schedule it to run at 11:55 pm each night.

`55 23 * * * /path/to/yourShellScript`


# Dependencies
Apache : https://httpd.apache.org/download.cgi#apache24

Mysql : https://dev.mysql.com/downloads/file/?id=482330

Php-Mysql : https://dev.mysql.com/downloads/repo/apt/

Php : https://www.php.net/distributions/php-7.0.33.tar.gz

# License

Use it if you want. I'd prefer if you cited me if you just copy paste, but I don't mind. Most of this code is pretty simple.
