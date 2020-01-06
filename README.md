
http://tmrh20.github.io/RF24Ethernet/ConfigAndSetup.html

# Configuration and Set-Up
RF24Ethernet requires the RF24 and RF24Network_DEV libraries (optionally RF24Mesh)
See http://tmrh20.github.io for documentation and downloads
See the video at https://www.youtube.com/watch?v=rBAIqAaRu0g for a walk-through of the software setup with Raspberry Pi and Arduino.

RPi

On the Raspberry Pi, a companion program, RF24Gateway must be installed along with the RF24 and RF24Network libraries

wget http://tmrh20.github.io/RF24Installer/RPi/install.sh 

chmod +x install.sh  

./install.sh  

cd RF24Gateway/examples/ncurses

make 

sudo ./RF24Gateway_ncurses 

The application will require the user to specify an IP address and Subnet Mask: 10.10.2.2 and 255.255.255.0 are the defaults with RF24Ethernet examples

Raspberry Pi defaults to the master node (00) using RF24Mesh. Secondary Raspberry pi nodes need to specify their RF24Network address or RF24Mesh nodeID.


Arduino

For Arduino devices, use the Arduino Library Manager to install the RF24 libraries

Open the included Getting_Started_SimpleServer or Getting_Started_SimpleClient example

Configure your chosen CE and CS pins for the radio connection.

Configure the RF24Mesh nodeID (Any unique value from 3 to 255)

Configure the IP address according to your preferences, (last octet must==nodeID) with the gateway set to the chosen IP of the RPi.

Connect into your nodes web-server at http://ip-of-your-node:1000 from the RPi or configure the client sketch to connect to a server running on the Raspberry Pi. 

Note: To minimize memory usage on Arduino, edit RF24Network_config.h with a text editor, and uncomment #define DISABLE_USER_PAYLOADS. This will disable standard RF24Network messages, and only allow external data, such as TCP/IP information.

Non-Raspberry Pi (Linux etc) Devices

Arduino can also function as a gateway for any Linux machine or PC/MAC that supports SLIP.

See the SLIP_Gateway and SLIP_InteractiveServer examples for usage without the need for a Raspberry Pi.

Accessing External Systems: Forwarding and Routing


In order to give your network or nodes access to your network or the internet beyond the RPi, it needs to be configured to route traffic between the networks.

Run

sudo sysctl -w net.ipv4.ip_forward=1 

to allow the RPi to forward requests between the network interfaces

sudo iptables -t nat -A POSTROUTING -j MASQUERADE 

to allow the RPi to perform NAT between the network interfaces

Note

This configuration is generally for initial testing only. Users may also need to add a static route to their local machine, or configure port forwarding on the RPi.

See the following links for more information on configuring and using IPTables:

http://www.karlrupp.net/en/computer/nat_tutorial
http://serverfault.com/questions/326493/basic-iptables-nat-port-forwarding

Warning

Note: Users are responsible to manage further routing rules along with their IP traffic in order to prevent unauthorized access.
