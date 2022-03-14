# DARAN
## Dynamic, Amateur, Radio Area Network

The following is taken directly from articles I posted to 147120.net before the site got broken. DARAN was originally called **Crossband Node Repeater Linking System**, or CNRLS. It has since been renamed DARAN. References to CNRLS are still in the original whitepapers which are presented here. I am editing these papers for appearance, correctness, and the reality of technical change. This is a work in progress, your comments and suggestions will be taken seriously.

**CNRLS** was originally conceived as a way to extend the range of a single repeater, but we quickly realized it would be a dynamic system that could extend the ranges of any repeaters within reach of CNRLS.


## CNRLS – Abstract
**Crossband Node Repeater Linking System - An Abstract for discussion**

**The Need -** Enhance the realized geographic range of the 147.120 N4LGH repeater beyond what simply raising the elevation of the current antenna could possibly accommodate, and allow Amateurs from areas outside of the 147.120 coverage area to participate in 147.120 on-air activities.

**The Idea -** A system consisting of multiple ‘Nodes’ to link repeaters in the Amateur 2M, 1.25M, and 70CM bands, providing extended coverage to existing repeaters by ‘linking’ them together over amateur frequencies.


**The Solution -** Programmable multi-radio multi-band ‘nodes’ placed in such a way that each node can maintain reliable communication with at least one other node, allowing for ‘crossband’ linking of repeaters within the range of complimenting nodes.


**Benefits -** Repeater linking, IoT device linking, crossband repeat for handheld and mobile range extension, beaconing, propagation study and very much more.

**Resources -** This is an ambitious project. Even with minimal nodes, considerable resources will be necessary. While considerable, it is doable with the team that appears to be available on the 147.120 repeater group. It will require hardware, site locations, programming, representation and coordination. It will require some funding which I have provided so far and have a plan to provide further funding as we progress.


### Repeater Linking Area Network (RLAN)

In effect this system creates a Repeater Linking Area Network comprised of the nodes in the system. A functional RLAN will be linked through one another having one or more nodes attached to the internet for communication with the CNRLS servers. 
 
 
### (Some) Theoretical Modes of Operation

**Crossband Repeat -** This mode can be standalone for the node, meaning only one node location is necessary for this mode and no communication with the system servers is necessary once the mode is set. Each node in the system could conceivably operate with complete independence in this mode. The node simply listens on one band and transmits received signals on another, effectively increasing the range of handheld and mobile stations to any repeater the node is able to communicate with, much like any other cross band repeat equipment. 


**Crossband Repeater Link -** This name may be somewhat misleading as each node is in itself a 'crossband' system; this MODE is crossband repeater linking. This mode is also able to be standalone, linking a repeater on one band to a repeater on either of the other bands.

**In Band Repeater Link -** This mode requires at least two nodes. Since no node will have a duplexer it will take a second band to form a link between two nodes. In this mode the two nodes will work in tandem to emulate a repeater with a duplexer by using two sites and an offband link. This facilitates the linking of two repeaters in the same band. It will be most common to link either two VHF or two UHF repeaters using a 222 MHz link. 

**Node to Node Crossband Repeat  -** This mode facilitates the linking of one or two two simplex frequencies in the same band. At least two nodes are required.

There are other 'modes' of operation, limited only by need and imagination. 

### Idle Mode Operations

While the nodes have no activity for their assigned tasks, their secondary task activities can be quite ranging. Beacon, scanning, activity reporting, signal strength readings, etc. With additional hardware, data such as temperature, pressure, and humidity can be telemetered to the CNRLS servers for later analysis. Questions we haven't thought to ask about propagation can be answered with the right queries to a database like this.
 
### (Some) Operation Notes

### User Interaction

A *user* should be able to interact with the system in any of several ways, depending upon their status with the system. 

Users should be able to access a web page and see what the current configuration of the system is. They should be able to see what settings are automatic and what settings they can change and what settings they cannot. 

They should be able to request certain functionality of the system and interact with or set other functionality. They should also be able to interact with the system in a limited way via DTMF, packet and digital formats.

*Managers* of the system should be able to maintain basic functions of the system such as control operations and certain types of user requests. This interaction should be able to take place online and via packet or DTMF.

*Administrators* should be able to access any part of the system and control all aspects of its operation in any way available.

For whatever user level is assigned, the system needs to be considerably flexible in its configuration. It needs an element of automation within certain rules and some manual control over various aspects of the system. There needs to be a system of menus to facilitate the configurations and automation rules. There needs to be a basic interface for display of system status, 

Most of the system needs to be able to be controlled on the air rather than over the internet or wifi. Users need to be able to notify the system of various requests and responses and the system needs to identify itself with an Amateur call during certain operational modes.

Nodes could announce their presence from time to time to allow non-connected amateurs the opportunity to locate and use the link and give instructions for its use.

 
### CNRLS – Operation
 
### Startup

**Node  -** Upon startup each node will determine if it has a direct internet connection. If it does, it will initiate communication with the 147120.net servers, which will assign a node designation to the station. It will then tune to a frequency determined by the servers and send a 'cq' via packet radio with an announcement that it is a 'root node' with an internet connection. 

If the node lacks its own internet connection, it will tune to a predetermined frequency and listen for a cq from a root node. If none is heard in a reasonable time, it will initiate its own cq via packet radio with an announcement that it needs a connection to a root node.

If a root node hears a cq, or its cq is answered from a non-root node it will accept a connection and ask for credentials. The root node will pass the credentials to the servers, which will assign a node designation for the non root node and pass it through the root node.

If a connected non root node hears an unconnected non root node call cq, it will answer the cq and announce that it is a connected non root node. If the unconnected non root node does not make a connection to a root node, it will call the connected non root node and the negotiation with the server will complete through this link.

Once the connection is established the servers will assign tasks to the nodes according to settings, schedules, conditions, activity, or many other considerations. This can be rather complex, and can provide a mountain of information if hardware is added to the nodes and telemetered data from those sensors is stored on the servers. 

In any case, if a node receives multiple connection offers it will choose the strongest one at the highest level.

**Server -** A server has to initialize at least once, and any time it needs to reboot. It will read a configuration file and proceed from there. On its first boot the configuration file will have been written by hand. Subsequent intentional reboots will have written a config file according to criteria determined at reboot time.

Once started the server will determine if there are any other servers running and if so, compare the configuration and determine if it is a primary or secondary server. If the server determines it is a primary server it will query existing nodes and call for any nodes not yet listed. If the server determines it is a secondary it will query the primary for the current list of nodes and verify it can communicate with them.

If a server determines it is secondary but cannot communicate with the primary, it will attempt to communicate with the nodes. It will query their current configuration and compare it with the last configuration sent to it from the primary. If the nodes' configurations are different from the previous config from the primary, the secondary will instruct the nodes to configure according to the primary's last config and take over as primary. 

When the original primary comes back online it will query the existing primary, accept its current config and request to take over as primary. If there are no pending operations the existing primary will transfer any current data streams and relinquish primary control. If there are pending operations, the existing primary will instruct the original primary to standby until it has completed the operation, and relinquish control once the operation is complete. If the secondary determines that the primary has lost internet connection a predetermined number of times within a predetermined period, it will request to remain primary when the malfunctioning primary comes back online and alert the administrator. 

It is acceptable to have only a primary server in a small to medium CNRLS system.
 
### Operation

Once registered with a server the nodes will report operational status and telemetered data as well as any on the air user requests. Idle mode operations will begin immediately or when programmed. 

**Online -** The server will be listening for connections from root nodes but it will also be running a web server through which users and administrators can interact with the system. A series of Status panels will present current configuration and measurement data as well as historical information including recent usage modes. A series of menus will allow administrators and to a limited extent users to control the configuration of the system. Telemetered data can be queried from the database using an API. Certain data milestones can be sent to social media such as 'tweeting' details about a connection change.

**On The Air -** Nodes will listen for command signals via DTMF and digital control codes on predetermined frequencies. These signals will trigger the node to request operational status settings from the server. The predetermined frequencies can be looked up on the web server pages and will be announced on node frequencies depending on the current mode of operation. IE a node configured to give a simplex crossband link into the 147.120 repeater operating on 222.5 mhz might announce "147.120 crossband link listening on 222.5 mhz PL 103.5" on 147.120 mhz. The node will only initiate these announcements on an idle channel.

Data accepted by the server by any means will then be processed and signaled to the nodes for operation. 


## CNRLS – Hardware

There is a plethora of equipment available that would accommodate the requirements of this description; the hardware described herein seems to be adequate for the application and is financially within the range of the community targeted by the project. It is conceivable that there will be several hardware configurations depending on requirements of a particular node. For now, all nodes will be built around the same basic devices.
 
**Nodes -**

**Radios -** The radio units used in the first prototypes and alpha production units are the <a title="RS-UV3A" href="https://www.hobbypcb.com/products/uhf-vhf-radio/rs-uv3a" target="_blank" rel="noopener noreferrer">RS-UV3A from HobbyPCB.com</a>. These units use a SOM that is used in other successful devices and has remarkable specs that are realized in operation. The devices are uniquely suited for this kind of operation. It has an option for a <a title="RS-UVPA" href="https://www.hobbypcb.com/products/uhf-vhf-radio/rs-uvpa" target="_blank" rel="noopener noreferrer">5 watt amplifier</a> add on that is capable of running all 3 bands.

Two such units will be used in each node. One unit would be equipped with the 5 watt amplifier and the other would run 'stock' with 250 mW output. Since most of the time one unit will be in receive and the other in transmit, only one amplifier module is necessary per node. EDIT: Since the amplifier also has extensive front end filtering, it may be necessary for the amplifier unit to be on both transceivers in various environments. WHile this increases cost, it increases selectivity and greatly enhances transmit capability.

**TNC -** Each radio in the node will have a <a title="Pi-TNC 2" href="https://nwradiosupply.com/products/tnc-pi-2" target="_blank" rel="noopener noreferrer">TNC</a> to accommodate Packet Radio digital communications. One could be adequate for communicating with nonconnected nodes but two will will facilitate a packet 'digipeater' that can be activated when convenient or required. This adds to the flexibility of the node but also allows simultaneous communications with multiple nodes.

**NOTE:** This hardware will probably not be implemented as KG4YDW suggests using <a title="Direwolf" href="https://github.com/wb2osz/direwolf" target="_blank" rel="noopener noreferrer">Direwolf</a> as a software TNC. Indeed it offers a lot of functionality that will be useful to the project.

**Processors -** Each node will have a Raspberry Pi *type* Single Board Computer. These SBC's will operate the radios, TNC, sensors, audio devices and power controller. They will do so under the supervision of the Primary Server. Currently, we're using variants that have the same IO pinout as the Raspberry Pi and are supported by the Armbian operating system. The <a title="Tinkerboard" href="https://www.asus.com/us/Single-Board-Computer/Tinker-Board/" target="_blank" rel="noopener noreferrer">Asus Tinkerboard</a> was seriously considered for the project but is somewhat expensive. The <a title="Odroid C2" href="https://www.hardkernel.com/shop/odroid-c2/" target="_blank" rel="noopener noreferrer">Hardkernel Odroid C2</a> (or th newer C4) is bing considered as it has excellent support from the manufacturer and  several third parties and is priced competitively with the Raspberry Pi. Several other Armbian supported boards appear to be appropriate as well. The decision to use Armbian will be discussed in the Software section.

**Controllers -** Nodes need audio and IO controllers in addition to the SBC. USB audio, fePi audio, and other audio and GPIO boards will be necessary to control the hardware. The Pi Repeater 2x is an excellent choice for a controller as it is already built for the RPi and repeater audio / GPIO.

**NOTE:** Now that Armbian supports RPi4, we will most likely use that platform along with the Pi2X controller.

**Sensors -** Each node will have various sensors that will be telemetered back to the servers. Sensors such as temperature, barometric pressure and humidity as well as others will be installed at each node to facilitate various propagation and field measurements at each node location. Uses for these sensors will be discussed in the Idle Mode Operations section. 

**Antennas -** So far the <a title="CX333" href="http://www.cometantenna.com/wp-content/uploads/2013/09/CX-333.pdf" target="_blank" rel="noopener noreferrer">Comet CX333</a> seems to be the most economic antenna that has decent gain and a reasonable price. While it is not as durable as a true 'repeater antenna' we are not a true repeater ... and most likely not to have a site as high as many repeaters. There is also a <a title="CR320B" href="https://www.diamondantenna.net/cr320bnmo.html" target="_blank" rel="noopener noreferrer">Diamond CR320B NMO</a> mount antenna that appears to be the best choice for sites that will have limited antenna capabilities. The CR320B is able to attach easily and near the transceiver location. 

**Enclosures -** Cabinetry will be dictated by the requirements of the particular node installation. Currently we are considering three cabinet configurations -

**Rack Mount -** Some locations will require rack mounting of the node equipment. The <a title="37-1U" href="https://www.circuitspecialists.com/rackmount-enclosure-37-1u.html" target="_blank" rel="noopener noreferrer">Circuit Specialist 37-1U</a> seems to be an inexpensive option. There are obviously many more options than this, please make not of any viable candidates in the comments section below.

**Shelf and Wall Mount -** Some locations will not have rack mounted equipment. Some will need the equipment mounted to a wall or left on a shelf. I have not yet explored this option.

**Tower Mount -** In some circumstances the equipment will be mounted near the antenna locations or exposed to the elements. There are several options for sealed units for these cases. I have not yet explored this option.

**Audio -** Since we are linking other radios we need to avoid any audio processing. Any processing should be done on the originating and destination stations. The RS-UV3A radios have good audio input and output hardware built in. All that would theoretically be necessary are the cables to interconnect them. Most of the control over audio will be in software. 

However, we will from time to time wish to inject audio to the stream, or 'announce' various information on the air. Audio can be input and output from a USB sound adapter or other mixing device. *(this section needs significant information added – Pi Repeater 2x)*

**USB Sound Device   -** see ICX Pi Repeater 2x. Nodes can be constructed using USB sound equipment or the integrated Pi2X controller.


## Servers
**Primary and Secondary -** Server hardware is a <a title="Odroid HC1" href="https://www.hardkernel.com/shop/odroid-hc1-home-cloud-one/" target="_blank" rel="noopener noreferrer">Hardkernel Odroid HC1</a> with a 128 GB SSD. It is inexpensive and extremely powerful. Including the SSD the cost of this unit is under $100. It has excellent ethernet speed and processing power. It is using Armbian as the operating system and is currently hosted by the <a title="Tech Party" href="http://www.tech-party.us" target="_blank" rel="noopener noreferrer">Central Florida Tech Party</a> on their system at <a title="Lilly's On The Lake" href="https://lillysonthelake.com/" target="_blank" rel="noopener noreferrer">Lilly's On The Lake</a>. This hardware is serving the page you are reading now.


### Interconnections

**Internet -** Each station can have a low data connection for direct connect to the internet. Packet will be the preferred method but one node needs to be connected. <a href="https://store.gl-inet.com/collections/travel-routers/products/gl-mifi-4g-smart-router" target="_blank" rel="noopener noreferrer">GL-Inet has a 'MiFi'</a> router and <a href="https://www.choiceiot.com/connectivity-services/iot-m2m-connectivity/" target="_blank" rel="noopener noreferrer">Choice</a> has low bandwidth inexpensive plans that would accommodate the requirement.


#### CNRLS – Software

### Crossband Node Repeater Linking System – Software 
 
**Common Components -** Both Server and Node will be constructed using similar Operating System and software. The details of this section must adhere to the details in the 'Operation' section of this paper.

**Operating System -** Both the server and node controllers will support the <a title="Armbian OS" href="https://www.armbian.com" target="_blank" rel="noopener noreferrer">Armbian</a> operating system. It is based on Debian and fairly optimized for the board it is implemented on. This is not an absolute necessity but support will only be given on this platform. A number of the boards supported by Armbian have identical GPIO outputs to the RPi and others have special signaling available. In any case, more than adequate IO information is available on any board chosen.

**Programming Language -** Language of choice can be anything that is easy to program for internet communication. We will be using Python as it seems to be perfectly suited for SBC hardware control and data-to-graphic display via the web. Using current releases on the various SBCs should keep the Python versions compatible.

Right now the following seems to be the place to start -Python's documentation<a href="https://docs.python.org/3/library/socketserver.html">https://docs.python.org/3/library/socketserver.html</a>

What seems to be a fairly complete tutorial for server and multiple clients<a href="https://realpython.com/python-sockets/">https://realpython.com/python-sockets/</a>

**DJango** seems to be the way to go with Python -<a href="https://www.djangoproject.com/">https://www.djangoproject.com/</a>


This guys demo is enlightening<a href="https://github.com/aschn/django-iot">https://github.com/aschn/django-iot</a>

A robust example?
<a href="https://github.com/electrocoder/iotdashboard">https://github.com/electrocoder/iotdashboard</a>
<a href="https://iothook.com/en/">https://iothook.com/en/</a>
<a href="https://iotdashboard.readthedocs.io/tr/latest/">https://iotdashboard.readthedocs.io/tr/latest/</a>

SPECIFIC data from Aidafruit for Python on C2 with Armbian<a href="https://learn.adafruit.com/circuitpython-libaries-linux-odroid-c2/circuitpython-odroid">https://learn.adafruit.com/circuitpython-libaries-linux-odroid-c2/circuitpython-odroid</a><a href="https://cdn-learn.adafruit.com/downloads/pdf/circuitpython-libaries-linux-odroid-c2.pdf">https://cdn-learn.adafruit.com/downloads/pdf/circuitpython-libaries-linux-odroid-c2.pdf</a> (PDF version)<a href="https://learn.adafruit.com/circuitpython-libaries-linux-odroid-c2/circuitpython-odroid"></a><a href="https://wiki.odroid.com/odroid-c2/application_note/gpio/wiringpi">https://wiki.odroid.com/odroid-c2/application_note/gpio/wiringpi</a> 

The 'Eric' Pythong Programming IDE has an option to create DJango projects…

Signaling codes will need to have a predictable format with room for expansion and customization. The basic formatting will be built around the code required for the RS-UV3A. It has a very well defined control set.

Additional node and system specific data can be wrapped around the base data. 

Server 
Web interface  
General Information  
System Status  
User Setting Requests  
System Administration  
Telemetry display
Internet sockets  
Nodes    
Data Streams (sensors)    
Connect, disconnect, transfer, etc.  
APIs    
Database requests    
database I/O streams
Security?
<a href="https://pypi.org/project/django-IoT-pki/">https://pypi.org/project/django-IoT-pki/</a> or so ...
julia high speed data processing on the server?
APRS for data transfer?
<a title="Direwolf" href="https://github.com/wb2osz/direwolf" target="_blank" rel="noopener noreferrer">Direwolf</a> instead of a 

hardware tnc?See specifically their APRStt Gateway<a title="User Guide" href="https://github.com/wb2osz/direwolf/blob/master/doc/User-Guide.pdf" target="_blank" rel="noopener noreferrer">User Guide</a> - There is an 

incredible amount of information here that is applicable to this project
<a title="HamLib" href="https://hamlib.github.io/" target="_blank" rel="noopener noreferrer">HamLib</a> for rig control?
Haven't EVEN considered what these things could tweet and so forth ... tweet current functionality? Tweet pending changes?
 
Node
 


CNRLS – Node Bring Up

CNRLS - node bring up
 
Currently using Armbian Armbian_5.86_Odroidc2_Debian_stretch_next_4.19.42
burn sd / emmc and boot, follow firstboot procedureNew user -  c2 / cnrls01
update / upgrade etc
armbian-config  date / time, timezone, ntp,  etc  remote desktop
