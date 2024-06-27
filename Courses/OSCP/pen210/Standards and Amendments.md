There are several different IEEE standards used to support the WiFi service.  The initial is [IEEE 802.11](https://en.wikipedia.org/wiki/IEEE_802.11).  This standard includes protocols for both Direct Sequence Spread Spectrum (DSSS) and Frequency Hopping Spread Spectrum (FHSS).  Collectively, these are used to manage  noise, interference  and jamming.  When utilised, channel will be 22 MHz wide.

As WiFi requires both transmitting and receiving, it can often result in a scenario when traffic effectively steps on each other.  This is referred to as a collision.  These standards include methods for avoiding these issues.

The 802.11 standard is for wireless LAN and the specification covers the physical layer and the Media Access Control (MAC).
The 802.11 committee has released amendments to the standards as wireless technology has advanced.  These will be covered through this course.
- 802.11 - original standard
- 802.11 a - up to 54 M/bit on 5 GHz
- 802.11 b - 5.5 M/bit and 11 M/bit on 2.4 GHz
- 802.11 g - up to 54 M/bit on 2.5 GHz, backwards compatible 802.11 b
- 802.11 h - regulatory requirement to limit power transmission in the 5 GHz band
- 802.11 i - provides enhanced security
- 802.11 n - provides higher throughput with multiple input/multiple output (MIMO) 
- 802.11 ac - very high throughput < 6 GHz , aka Wi-Fi 5
- 802.11 ad - multi-gigabit in the 60 Hz band know as WiGig
- 802.11 ax - high efficiency (HE) wireless LAN  AKA Wi-Fi 6
## The IEEE 802.11 Standard
The purpose of this section is to provide an understanding of the various protocols and the differences between them.  It is not necessary to memorise them but knowing which standard our device supports and what frequencies it covers is important. 
### 802.11 a
The 802.11 a standard uses the 5 GHz band which offers more channels which do not overlap as much as other standards in the 802.11 suite.  It uses Orthogonal Frequency-Division Multiplexing (OFDM) modulation  to provide transfer rates of up to 54 MBit/s, using 20 MHz channels.

Simply put, OFDM divides each channel into multiple 'subchannels', and then encodes data across multiple carrier frequencies at once.  We normally refer to these subchannels as subcarriers but they are also called tones.
### Multiple Input Multiple Output
### Greenfield Mode
### Antennas 
The number of streams and therefore the rates that can be reached depends on the number of antennas on the transmitter and receiver.  The notation format is txr:s:
- t. is the number of transmit  (TX) chains;
- r. is the number of receiving (RX) chains;  and
- s. is the maximum number of spatial streams the radio can use.
### Modulation and Coding Scheme
802.11 n uses different modulations, coding rates, and streams to achieve speeds of up to 600 Mbit.  A Modulation and Coding Scheme (MCS) rate is just a number that refers to a specific modulation and coding rate and in the case of 802.11 n, the number of spatial streams in use.
## Wireless Networks
### Infrastructure
All WiFi networks must have at least 1 Access Point (AP) and one Station (STA).  These two form a Basic Service Set (BSS).   The AP is usually connected to a connected to a wired network, called the Distribution System (DS).  A very simple example of this would be a station, such as a laptop or smartphone, connected to a wireless access point which is connected via an Ethernet cable to a wired router.  This sort of setup is what you might find in most homes.  

When a set of two or more wireless APs are connected to the same wired network, we call this an Extended Service Set (ESS).  Each additional AP defines a single logical network segment.    
### Wireless Distribution Systems
In wireless systems where the router and the AP functions are integrated, the DS would be anything other than the wireless network itself.  A Wireless Distribution System (WDS)  on the other hand is just what it sounds like.  It is a DS going over WiFi instead of a cable.  WDS have two connectivity modes:
1.  Wireless Bridging: Only allows WDS APs to communicate with each other; and 
2. Wireless Repeating: Allows both stations and APs to communicate with each other.

An additional use case could include an area of an office which is too far away from the AP to receive a string signal.  This issue could be addressed by installing an additional AP without running a cable to it.  The computer in the area that doesn't receive sufficient signal will connect to the new AP, which carries the signal to the first AP.  This arrangement uses the same channel as the existing AP for back-haul.  This channel sharing has an impact on high-traffic networks as the available data rates can be cut in half.  In low traffic networks, this is unlikely to be an issue.
### Ad-hoc networks
An ad-hoc network is not common, however, relevant to WiFi security.  An ad-hoc network , also known as a Independent Basic Service Set (IBSS), consists of at least two stations connected without an AP.  In an ad-hoc network, one of the participating stations takes on some of the responsibilities of an AP, such as beaconing and authentication of new clients joining the network.  The station taking on the role of the AP does not relay packets to other nodes like and AP does.
### Ad-hoc demo
Ad-hoc demo is a deviation from a standard ad-hoc or IBSS mode.  This mode allows a pseudo-IBSS because its a pre-standard, pre-IBSS mode with just data.
There are no management frames whatsoever and the BSSID is all zeros.
There are a number of pros and cons to ad-hoc demo mode.  It could be seen as raw or bare ad-hoc mode.  As such , we have to set the rate manually on all wireless cards.  The lack of management frames and collision avoidance mechanisms allow for a slightly higher throughput, but it requires a clear channel or strong signal.
### Mesh networks
Mesh networks are essentially a collection of AP repeaters, which can be used to extend a network when it isn't feasible to use cables to add additional APs.  In a mesh network, additional APs act as both client and  as an AP to repeat the network signal.  This is considered in the 802.11 s standard.

In addition to the similarities with infrastructure networks, the 802.11 s standard adds the following device classes:

-  Mesh Point (MP): devices that establish a link between mesh devices.  These can be either Mesh Portals, Mesh APs or even other Mesh Points;
- Mesh AP (MAP): devices that have the functionality of a mesh point and an AP; and
- Mesh Portal (MPP): devices that provide a link between the wired network and the wireless network.
Its relevant to mention that some devices in a wireless network can disappear from the network, consequently the path that a packet takes can change.  The path is dynamically generated by software that takes various changing parameters into account such as signal quality, noise, rate, response time and distance between nodes.

Since mesh networks are peer to peer, they have to handle neighbor discovery, connecting to peers and security between each other.  After discovering neighbor MAPs, they start peering.  
There are two peering modes available:
- Mesh Peering Management  (MPM): Insecure peering; and
- Authenticated Mesh Peering Exchange (AMPE): Secure peering.

MPM is unencrypted and rouge stations may hijack connections.

AMPE, the encrypted protocol, uses Simultaneous Authentication of Equals (SAE) or 802.1x to exchange encryption keys.  SAE is a password based authentication mechanism whereas 802.1x uses an authentication server.  
### WiFi Direct
WiFi direct provides a single hop communication between devices.  For example, a connection between a laptop and a printer can be direct, rather than through an AP.  This can be the case, even if they are connected to the same WiFi network.  WiFi direct is also referred to as WiFi P2P.  
### Monitor Mode
Monitor mode is not a wireless mode or architecture scheme, but rather a state of a wireless device that allows it to monitor all WiFi signals within its range.
A wireless device (card) that is in Monitor Mode can see and all network traffic between all devices and AP across all networks within range.
## WiFi Encryption
WiFi works over radio waves which makes it subject to eavesdropping and therefore encryption has to be used to protect the transmitted data.

Wired Equivalent Privacy (WEP) was created when the 802.11 standard was released in order to give privacy features similar to those found in wired networks.
WEP is considered to be insecure and easily compromised, consequently, the IEEE created a new group called 802.11 i aimed at improving WiFi security.  WiFi Protected Access (WPA) superseded 
WEP.  This was subsequently followed by WPA2.

Additionally, technologies from various vendors allowed users to securely share the passphrases on devices to be added to the network without having to type it.  WiFi Protected Setup (WPS) was released to standardise it.

WPA3 was first announced in January 2018 and released in June the same year.  It doesn't replace any existing security solution, rather aims to solve a few key problems with the following:
- Forward secrecy using a dragonfly handshake with SAE;
- Simplify process of configuring devices with no display (IOT);
- A new 192-bit mode for enterprise networks with stronger cipher suites; and
- Mandatory use of Protected Management Frames (PMF), from 802.11 w.

Opportunistic Wireless Encryption (OWE), also known as 'Enhanced Opened', adds encryption to public WiFi networks.
### Open Wireless Networks
Open Wireless Networks  do not involve any encryption and therefore anyone running a wireless sniffer can see the traffic as-is.  
Open Wireless Networks are susceptible to eavesdropping as the traffic on them is unencrypted.  WEP aims at providing some degree of privacy to data exchanged on the wireless network.  WEP uses the Rivest Cipher 4 (RC4) to encrypt traffic and performs CRC32 checksums for message integrity.  
### WPA Network Connection
A WPA secure network communication channel is setup in four steps:
- Agreement on security protocols;
- Authentication;
- Key distribution and verification; and
- Data encryption and integrity.
[^1]: Verification and Validation are separate concepts which when used together support assessing the quality of a system.  Verification is the process of assessing whether a system complies with its relevant specification.  Validation is the process of assessing whether a system meets the needs of its identified stakeholders.

[4 way handshake](/home/kali/workspaces/Notes/images/wpa_4_handshake.png)
#### Security Protocols
The different types of security protocols that are supported by the AP are provided in its beacons.  The station sends probe requests in order to receive network information (rates, encryption, channels e.t.c.).  It will then join the by using open authentication followed by association where it indicates which ciphers will be used. 
#### WPA Authentication
This step is only used in enterprise configurations and is based on the Extensible Authentication Protocol (EAP) .  It can be established with the following:
- EAP-Transport Layer Security  (TLS);
- EAP-Tunneled Transport Layer Security (TTLS); and
- Protected Extensible Authentication Protocol (PEAP) for hybrid authentication where only the server certificate is required.
Depending on the authentication method selected, several messages are exchanged between the Station and AP.  Eventually, a Master Key (MK) is generated.  It this is successful a 'Radius Accept' message is sent to the AP containing the MK and another message, an EAP message sent to the client indicating success. 

The third phase of the authentication process is the exchange of different keys used for authentication, message integrity and message encryption.  This is done via the 4 way handshake to exchange the Pairwise Transient Key (PTK) and the Group Temporal Key (GTK). This allows for:
- Confirmation of the cipher suite used;
- Confirmation of the PMK knowledge by the client;
- Installation of the integrity and encryption keys; and
- Send GTK securely.

Broadly speaking, the 4 way handshake works as follows:
- The authenticator sends a nonce called (ANonce); 
- The supplicant creates the PTK and sends it nonce called SNonce with the MIC.  After the construction of the PTK, it will check if the supplicant has the right PMK.  If the MIC check fails, the supplicant has the PMK;
- The message from the authenticator to the supplicant will contain, WPA2/3 is used, the current GTK.  This key is used to decrypt multicast/broadcast traffic.  It that message fails to be received, it is re-sent; and
- Finally, the supplicant sends an acknowledgement to the authenticator.  The supplicant installs the keys and starts the encryption.
### Wireless Protected Setup
Also know as WiFi Simple Configuration, the protocol allows users to pair devices to a network without having to add the ESSID and or its passphrase.

#### WPS Architecture
WPS defines 3 components:
- Enrollee; a device seeking to join a WLAN;
- Access point; and
- Registrar.
There are three interfaces:
- E; logically located between the enrollee and the registrar.  The purpose is for the registrar to issue credentials to an enrollee.
- M; the interface between the registrar and the access point.  It manages and configures the access point; and
- A; enables the discovery of WPS access points (via IE in beacons) and for external registrars, enables communications between the enrollees and the registrars.








