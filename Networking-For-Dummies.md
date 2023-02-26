NETWORKING FOR DUMMIES

# OSI Model
:osi:overview:

The OSI Reference Model establishes a hierarchy for protocols so that each protocol can deal with just one part of the overall task of data communications.

    * Physical      (layer 1): Describes the mechanical and electrical details of network components such as cables, connectors, and network interfaces.
    * Data link     (layer 2): Describes the basic techniques that networks use to uniquely identify devices on the network (typically via a MAC address) and the means for one device to send information over the physical layer to another device, in the form of data packets. Switches operate at the data link layer, which means that they manage the efficient transmission of data packets from one device to another.
    * Network       (layer 3): Handles the routing of data across networks. Routers operate at the network layer.
    * Transport     (layer 4): Provides for reliable delivery of packets.
    * Session       (layer 5): Establishes sessions between network applications.
    * Presentation  (layer 6): Converts data so that systems that use different data formats can exchange information.
    * Application   (layer 7): Allows applications to request network services.

# Cables

Cat-5e cable is able to carry network data at speeds of up to 1 gigabit per second (Gbps) for 100 meters max. The newer and somewhat more expensive Cat-6 cable can carry data at up to 10 Gbps but can sustain that speed for only 55 meters 

# Ethernet

An Ethernet packet contains the following information:

    * Preamble:                The preamble consists of 56 bits of alternating ones and zeros and is used to synchronize the precise timing required to read packet data.
    * Start-of-frame marker:   A start-of-frame marker is a single byte that indicates that the frame is about to begin.
    * Destination MAC address: (six bytes).
    * Sender MAC address:      (six bytes).
    * Tag:                     The tag, which is used to support virtual local area networks (VLANs), is optional. A VLAN lets you divide two or more distinct LANs on a shared physical infrastructure (for example, cables and switches). (For more information about VLANs, see Chapter 3 of this minibook, as well as Book 3, Chapter 1.)
    * Ethertype (two bytes):   This field indicates the specific protocol that is contained in the payload.
    * Payload:                 The payload contains the actual data being sent by the packet. The payload can be anywhere from 46 to 1,500 bytes. If the information that needs to be sent is longer than 1,500 bytes, the information must be broken into two or more packets, sent separately, and then reassembled when the packets reach their destination. (The tasks of breaking up and reassembling the data are handled by protocols at higher layers in the OSI framework; Ethernet itself has no understanding of what is in the packets it sends.)
    * Frame check sequence:    (four bytes) The frame check sequence (FCS) is used to ensure that the frame data was sent correctly. Basically, the interface that sends the packet uses an algorithm to calculate a four-byte number based on the contents of the frame and saves this number in the FCS field. When the packet is received, the receiving interface repeats the calculation, and then makes sure that the number recorded in the FCS portion of the packet matches the number it calculated. If the numbers disagree, it means the packet got garbled in transmission and is discarded.

Note that the details of an Ethernet packet are not really of much concern when you design and implement a network. Here are the main points to remember:

    * Ethernet packets contain the MAC addresses of the sender and the receiver.
    * The payload of an Ethernet packet is almost always a packet created by another higher-level protocol such as IP.
    * Ethernet packets can contain a tag field used to implement VLANs, which provide an important means of organizing a large network into smaller parts that can be more easily managed.

Broadcast packet is sent to ff-ff-ff-ff-ff-ff, received by all, but only receiver or DHCP will reply (ex: device connecting to a network for the first time).

Wireless has very similar mechanism with the WAP instead of a switch. Though it doesn't have a wireless switching capability. Therefore WAP is like a wireless hub.

Switches maintain MAC address tables based on the packets received, since packets contain sender MAC address, it is recorded for that port. If more than one device are connected on a specific port (as in the case of a second switch) they all are recorded for that port. This is called learning. Forwarding is when switch sends packet to the destination port as is. Flooding is when switch receives packet for MAC it doesn't know, so it floods all ports (as they might have more than one device attached to them)

    * Learning: The switch learns what devices are reachable on each of its ports.
    * Forwarding: The switch forwards incoming packets just to the correct port based on the intended destination.
    * Flooding: The switch forwards incoming packets to all ports when it hasn’t yet learned how to reach the intended destination

A collision domain is a segment of a network on which collisions are possible. Eg. Packets sent at the same time.

Bridges are sometimes used to connect different types of networks (cat-5 and fiber-optical). Switches also do that for the different speeds ports (printer etc 100 mbps vs 1Gbps computer)

You can also use for that SFP small form factor pluggable ports which are pluggable and support higher speeds. Ex: on server or uplink switch.

Broadcast domain is the segment of the network for which the broadcast packet is intended.

ARP (address resolution protocol) request is sent when one IP wants to send.

Collisions can be reduced by using routers or by using VLANs.

A router differs from a switch in the following ways:

    * Switches work with MAC addresses and know nothing about IP addresses. In contrast, routers work with IP addresses.
    * Routers can facilitate communication between IP networks with different subnets. For example, if your organization has a 10.0.100.x network and a 192.168.0.x network, a router can enable packets to get from the 10.0.100.x network to the 192.168.0.x network, and vice versa. A switch can’t do that. (For more about subnets, refer to Book 2, Chapter 3.)
    * Routers also enable a private network to communicate with the Internet. For example, suppose you want to connect your network to the Internet via a broadband cable provider such as Comcast. The cable provider will give you a network interface that has a public IP address. You must then use a router to exchange packets from your private network to the Internet via the public IP address. A switch can’t do that for you.
    * Switches split up collision domains. The segments created by switches are still part of the same broadcast domain. In contrast, routers split up broadcast domains. So, broadcast packets do not cross the boundaries created by routers. (Actually, as I explain in the “Understanding VLANs” section, later in this chapter, switches can also break up broadcast domains.)
    * Switches typically have a large number of ports — often as many as 48 in a single switch. Routers usually have fewer ports, typically between two and eight. (However, routers for very large networks may have many more ports. For example, Cisco makes a router that can accommodate as many as 256 ports in a single chassis.)

# NAT (Network address Translation)

Router (when packet is sent out to the internet) substitutes the IP address of the sender with it's own and keeps track of what it sent. On the way in, the process is reversed.

# VPN

A virtual private network (VPN) is a secure connection between two private networks over a public network (in other words, over the Internet). All the data that flows over the VPN is encrypted.

There are two common uses for VPNs:

    * To provide remote workers with secure access to your company network: To do that, you set up a VPN on the router, and then provide your remote workers with the credentials necessary to access the VPN. The remote workers can run a software VPN client on their home computers or laptops to connect to your company network.
    * To establish a tunnel directly between routers on two networks that are separated geographically: For example, suppose you have offices in Los Angeles and Las Vegas. You can use routers on both networks to establish a VPN tunnel between them. This effectively joins the networks together, so that devices on the Los Angeles network can freely exchange packets with devices on the Las Vegas network, and vice versa.

# VLANs

Virtual Local Area Network.  If (or when) your network grows large enough that you want to set up two or more subnets to better manage it, you’ll probably also want to set up two or more VLANs, one for each of your subnets.

A VLAN can divide a single switch into two virtual switches that behave exactly as if they were separate switches. This means the following:

    * If a port on one VLAN receives a packet intended for a destination on the same VLAN, the switch forwards the packet to the destination port, the same as if VLANs were not in use.
    * When a port on one VLAN receives a packet intended for a destination on the same VLAN that the switch has not yet learned, the switch will flood only those ports that are on the destination VLAN — not all the ports on the switch. Thus, VLANs can reduce traffic caused by flooding.
    *  When a broadcast packet is received, the switch will forward the packet only to those ports that are on the same VLAN. In other words, VLANs can break up broadcast domains in the same way that a router can.
    * If a port on one VLAN receives a packet intended for a different VLAN, a router is required to link the networks. That’s because separate VLANs are, for all intents and purposes, separate networks.

That being said, most switches that support VLANs also support trunk ports, which can switch traffic between VLANs. A trunk port is a port that can handle traffic for two or more VLANs.

Access port - port that is configured to operate on one VLAN only.

Trunk port - port this is configured to operate on multiple VLANs.

You can configure ports on different switches to be a part of the same VLAN.

# Servers

Preferably a server should have multiple network interfaces as a failover.

## Network services

DHCP (dynamic host configuration protocol) - service which recognized devices on the network and provides them with an address.

DNS (domain name system) - enables people to use human readable names instead of IPS.

## File Sharing

## Multitasking

Server should have the ability to execute multiple processes at the same time. In reality this depends on the number of CPUs (more than one).

## Directory Services

Network directories provide information about the resources that are available on the network: users, computers, printers, shared folders, and files.

Active Directory (basically an authentication system) is a database that organizes information about a network and all its computers and users. It’s simple enough to use for networks with just a few computers and users, but powerful enough to work with large networks containing tens of thousands of computers and users.

## Security services

    * Establish password policies. For example, you can mandate that passwords have a minimum length and include a mix of letters and numerals.
    * Set passwords to expire after a certain number of days. Network users must change their passwords frequently.
    * Encrypt network data. A data-encryption capability scrambles data before it’s sent over the network or saved on disk, making unauthorized use a lot more difficult. Good encryption is the key to setting up a virtual private network (VPN), which enables network users to securely access a network from a remote location by using an Internet connection.
    * Manage digital certificates. Digital certficates are used to ensure that users are who they say they are and les are what they claim to be

## Important features

    * Scalability: The ability to increase the size and capacity of the server computer without unreasonable hassle
    * Reliability: if a server fails more than one person is affected. Many servers have redundant components (power, CPU..)
    * Availability: how long does it take to correct the problem? server components should be easily troubleshoot-able by design, and even hot-swappable if possible. Best is fault-tolerant.
    * Service and support: it should be on site, not for you to take to repair shop.

## Components of a server

Similar to client computers, but higher quality.
:server:motherboard:cpu:ram:hd:ssd:nic:video:power:kvm:

    * Motherboard: is the computer’s main electronic circuit board to which all the other components of your computer are connected. With major components processor (CPU); supporting circuitry (the chipset); memory (RAM); expansion slots; a hard drive controller; USB ports for devices such as keyboards and mice; a graphics adapter; and one or more network interfaces.
    * Processor: CPUs come in two basic mounting styles: slot or socket. However, you can choose from several types of slots and sockets. Some motherboards support multiple CPUs. Most important part in processor is multitasking. This depends on how many cores you have and that they support hyper-threading (handling 2 threads at a time).
    * Memory: the more RAM the better. But motherboard should be compatible with the amount of RAM installed.
    * Hard Drive: sata is cheap consumer grade. SCSI, or Serial Attached SCSI are better.  SSD are best, they have no mechanical parts and are faster.
    * Network interfaces: ideally at least 2 for a failover
    * Video: save here. Cheap built in interface will suffice
    * Power supply: should be a larger one (600 w) because many devices are attached to it. Should have a second power supply, as this part fails more often. 

KVM switch: allows to connect multiple servers to one keyboard, monitor (video) and mouse.

# Cloud Computing

Examples:

* Email services:
    * Traditional: Provide email services by installing Microsoft Exchange on a local server computer. Then your clients can connect using Microsoft Outlook to connect to the Exchange server to send and receive email.
    * Cloud: Contract with an Internet-based email provider, such as Google Mail (Gmail) or Microsoft’s Exchange Online. Cloud-based email services typically charge a low monthly per-user fee, so the amount you pay for your email service depends solely on the number of email users you have.

* Disk storage:
    * Traditional: Set up a local file server computer with a large amount of shared disk space.
    * Cloud: Sign up for an Internet file storage service and then store your data on the Internet. Cloud-based file storage typically charges a small monthly per-gigabyte fee, so you pay only for the storage you use. The disk capacity of cloud-based storage is essentially unlimited.

* Accounting services
    * Traditional: Purchase expensive accounting software and install it on a local server computer.
    * Cloud: Sign up for a web-based accounting service. Then all your accounting data is saved and managed on the provider’s servers, not on yours.

Benefits:

    cost effective (20%)
    Scalable
    Reliable
    Hassle free
    Globally accessible

Drawbacks:

* Entrenched applications: Your organization may depend on entrenched applications that don’t lend themselves especially well to cloud computing — or that at least require significant conversion efforts to migrate to the cloud. For example, you might use an accounting system that relies on local file storage.

Fortunately, many cloud providers offer assistance with this migration. And in many cases, the same application that you run locally can be run in the cloud, so no conversion is necessary.

* Internet connection speed: Cloud computing shifts much of the burden of your network to your Internet connection. Your users used to access their data on local file servers over gigabit-speed connections; now they must access data over slower bandwidth Internet connections. Upgrading connection is a cost.

* Internet connection reliability: The cloud resources you access may feature all the redundancy in the world, but if your users access the cloud through a single Internet connection, that connection becomes a key point of vulnerability. Should it fail, any applications that depend on the cloud will be unavailable. If those applications are mission-critical, business will come to a halt until the connection is restored.

Here are two ways to mitigate this risk:

    * Make sure that you’re using an enterprise-class Internet connection. Enterprise- class connections are more expensive but provide much better fault tolerance and repair service than consumer-class connections do.
    * Provide redundant connections if you can. That way, if one connection fails, traffic can be rerouted through alternative connections.

Security threats: You can bet your life that hackers throughout the world are continually probing for ways to break through the security perimeter of all the major cloud providers. When they do, your data may be exposed.

The best way to mitigate this threat is to ensure that strong password policies are enforced.

# Types of Cloud Services

Applications (SaaS). Ex: G-Suite vs MS Office (local)

Platforms (PaaS). Ex: AWS vs local server

Services (infrastructure, IaaS).

Public Cloud - G-Suite.

Private Cloud - Cloud services on local network.

Hybrid cloud - mix of the two.

# Moving to Cloud

* Don’t depend on a poor Internet connection. First and foremost, before you take any of your network operations to the cloud, make sure that you’re not using consumer-grade internet connection. spend the money for a high-speed enterprise-class connection that can scale as your dependence on it increases.

* Assess what applications you may already have running on the cloud. If you use Gmail rather than Exchange for your email, congratulations! You’ve already embraced the cloud. Other examples of cloud services that you may already be using include a remote web or FTP host, Dropbox or another file-sharing service, Carbonite or another online backup service, a payroll service, and so on.

* Don’t move to the cloud all at once. Start by identifying a single application that lends itself to the cloud. If youare engineering rm archives projects when they close and wants to get them to your primary file server but keep them readily available, look to the cloud for a file storage service.

* Go with a reputable company. Google, Amazon, and Microsoft are all huge companies with proven track records in cloud computing. Many other large and established companies also offer cloud services. Don’t stake your company’s future on a company that didn’t exist six months ago.

* Research, research, research. Pour yourself into the web, and buy a few books. Hybrid Cloud For Dummies, by Judith Hurwitz, Marcia Kaufman, Dr. Fern Halper, and Daniel Kirsch (Wiley), is a good place to start.

# Protocols
:osi:details:

TCP/IP: internet and LANs. Originally for Unix.

Ethernet: low level "electrical" protocol.

IPX/SPX:

Standards (orgs):

* American National Standards Institute (ANSI): The official standards organization in the United States. ANSI is pronounced AN-see. www.ansi.org

* Institute of Electrical and Electronics Engineers (IEEE): An international organization that publishes several key networking standards — in particular, the official standard for the Ethernet networking system (known officially as IEEE 802.3). IEEE is pronounced eye-triple-E. www.ieee.org

*  International Organization for Standardization (ISO): A federation of more than 100 standards organizations throughout the world. If I had studied French in high school, I’d probably understand why the acronym for International Organization for Standardization is ISO, and not IOS. www.iso.org
*  Internet Engineering Task Force (IETF): The organization responsible for the protocols that drive the Internet. www.ietf.org

*  World Wide Web Consortium (W3C): An international organization that handles the development of standards for the World Wide Web. www.w3.org


## Datalink layer

CSMA/CD (Carrier Sense Multiple Access/Collision Detection) for Ethernet and token passing for Ring networks, both designed to ensure that data is passed around uncorrupted, without interference. When the network reaches 30 computers, you need to split it into separate collision domains.

## Network layer

Responsible for routing packets.

Most protocols divide the logical address into two parts:
    1. Network address: Identifies which network the device resides on.
    2. Device address: Identifies the device on that network.

In a typical IP address — say, 192.168.1.102 — the network address is 192.168.1, and the device address (called a host address in IP) is 102.

Routing happens when the message is sent from one network to another.

## Transport layer

TL is responsible for ensuring safe transportation of packets from one computer to another. TCP is connection oriented protocol. Ex: acknowledgement messages, resending packets.

UDP is connectionless (designed for speed and efficiency, not reliability). It simply sends the data.

## Session layer

A session is an exchange of connection-oriented transmissions between two network devices. Each transmission is handled by the transport layer protocol. The session itself is managed by the session layer protocol.

The session layer allows three types of transmission modes:
    * Simplex: Data flows in only one direction.
    * Half-duplex: Data flows in both directions, but only in one direction at a time.
    * Full-duplex: Data flows in both directions at the same time

Many protocols function on all 3 upper layers: session, presentation, application. Ex SMB for file sharing.

## Presentation layer

Utf-8

PL converts data between formats, compresses / decompresses The data and encrypts / unencrypts it.

## Application layer

This is the API.

Well known protocols:
    * Domain Name System (DNS): For resolving Internet domain names
    * File Transfer Protocol (FTP): For file transfers
    * Simple Mail Transfer Protocol (SMTP): For email
    * Server Message Block (SMB): For file sharing in Windows networks
    * Network File System (NFS): For file sharing in Unix networks
    * Telnet: For terminal emulation

## Ethernet

Transmission speed of Ethernet is measured in millions of bits per second (Mbps) or billions of bits per second (Gbps). Ethernet comes in several different speed versions:
    * Standard Ethernet: 10 Mbps; rarely (if ever) used today.
    * Fast Ethernet: 100 Mbps; still used for devices where speed is not particularly important, such as printers or fax machines.
    * Gigabit Ethernet and beyond: 1,000 Mbps; the most common speed used to connect user computers to a network. Faster speeds, such as 10 Gbps, 100 Gbps, and even faster, are sometimes used in high-speed networks to connect servers and other critical devices to the network.

## IP

Internet Protocol is a logical addressing.

ARP (address resolution Protocol) is used for converting IP to MAC.

## TCP

Transmission Control Protocol: One-to-one connections (not broadcast).

## UDP

User Datagram Protocol: connectionless Protocol. DNS uses UDP to look up IP address of a domain name. DNS server replies with the IP over UDP as well.

Latest Internet statistics from ISC: https://www.isc.org/network/survey (discontinue due to IPv4 only).

Distinct types of networks on the internet:
    * Government agencies, such as the Library of Congress and the White House;
    * military sites,
    * educational institutions, such as universities and colleges (and their libraries);
    * businesses, such as Microsoft and IBM;
    * ISPs, which allow individuals to access the Internet;
    * and commercial online services, such as America Online and MSN

## Standards

RFCs represent Internet standards, which are agreed upon by everyone. The various types of RFC (request for comments) documents from the IETF website (www.ietf.org):
    * Internet Standards Track: This type of RFC represents an Internet standard. Standards Track RFCs have one of three maturity levels, as described in Table 2-1. An RFC enters circulation with Proposed Standard status but may be elevated to Draft Standard status — and, ultimately, to Internet Standard status.
    * Experimental specifications: These are a result of research or development efforts. They’re not intended to be standards, but the information they contain may be of use to the Internet community.
    * Informational specifications: These simply provide general information for the Internet community.
    * Historic specifications: These RFCs have been superseded by a more recent RFC and are thus considered obsolete.
    * Best Current Practice (BCP): RFCs are documents that summarize the consensus of the Internet community’s opinion on the best way to perform an operation or procedure. BCPs are guidelines, not standards.

# Binary

1 0 1 1 = 1*2^3 + 1*2^2 + 1*2^1 + 1*2^0

It's all about powers of 2 starting with 2^0 from right to left multiplied by the value of he bit in that position.

Because of that:

K represents 2^10 (1,024).

M in MB stands for 2^20, or 1,024K

G in GB represents 2^30, which is 1,024MB 


## Logical operations
:and:or:xor:not:

    * AND: Compares two binary values. If both values are 1, the result of the AND operation is 1. If one or both of the values are 0, the result is 0.
    * OR: Compares two binary values. If at least one value is 1, the result of the OR operation is 1. If both values are 0, the result is 0.
    * XOR: Compares two binary values. If one of them is 1, the result is 1. If both values are 0 or if both values are 1, the result is 0.
    * NOT: Doesn’t compare two values but simply changes the value of a single binary value. If the original value is 1, NOT returns 0. If the original value is 0, NOT returns 1.

To apply these operations to binary, line up the two binary numbers and apply the logical operation to one bit at a time (same position bit, when applying to two binary numbers)

Octet - 8 bits

:ip:explained:
IP address has 4 octets, sometimes referred to by w, x, y, z (left octet to right)

For the host ID octet, the 00000000 and 11111111 (0 and 255) are reserved (0 represents the network, 255 is for broadcast).


# Classes
:ip:classes:

A: 1–126.x.y.z /8

    For large networks. 1st octet is the network, rest are (~16M) hosts

    Most left bit is always 0, therefore the mask is 255.0.0.0

B: 128–191.x.y.z /16

    1st + 2nd octet are the network, rest (~65K) are hosts

    Most left 2 bits are always 10, therefore the mask is 255.255.0.0

C: 192–223.x.y.z /24

    1st+2nd+3rd are the network, rest (254) are hosts

    Most left 3 bits are always 110, therefore the mask is 255.255.255.0

D, E: reserved

127.x.y.z - loopback

# Subnetting
:ip:subnet:mask:cidr:

Subnetting provides a more flexible way to designate which portion of an IP address represents the network ID and which portion represents the host ID. With standard IP address classes, only three possible network ID sizes exist: 8 bits for Class A, 16 bits for Class B, and 24 bits for Class C. Subnetting lets you select an arbitrary number of bits to use for the network ID.

The way TCP/IP works dictates that all the computers with the same network ID must be on the same physical network. The physical network comprises a single broadcast domain, which means that a single network medium must carry all the traffic for the network. For performance reasons networks are broken up into smaller than class C subnets.

## Subnet mask

SM is another 32 bit number, which always starts with 255 octet (and that is not a valid IP address range). Those IP address bits that represent the network ID are represented by a 1 in the mask, and those bits that represent the host ID appear as a 0 in the mask. As a result, a subnet mask always has a consecutive string of ones on the left, followed by a string of zeros.

Ex: 11111111 11111111 11110000 00000000

Here the 1s are the 16 bits of network ID + 4 bits of subnet, 20 in all, are the complete network ID.

CIDR (classless interdomain routing): this is a shorthand which is added at the end of IP address to indicate the number of complete Network ID bits. In this case /20.

Here is how routers extract network ID:

144 . 28 . 16 . 17
IP address: 10010000 00011100 00010000 00010001

Logical AND (if both sides are 1 then result is one, otherwise 0)

Subnet mask: 11111111 11111111 11110000 00000000 (255.255.240.0)

Result:

Network ID: 10010000 00011100 00010000 00000000

144 . 28 . 16 . 0

Additional subnetting rules:
    * The minimum number of network ID bits is eight. As a result, the first octet of a subnet mask is always 255.
    * The maximum number of network ID bits is 30. You have to leave at least two bits for the host ID portion of the address to allow for at least two hosts.
        * If you use all 32 bits for the network ID, that leaves no bits for the host ID. Obviously, that won’t work.
        * Leaving just one bit for the host ID won’t work, either, because a host ID of all ones is reserved for a broadcast address, and all zeros refers to the network itself.
        * Thus, if you use 31 bits for the network ID and leave only 1 for the host ID, host ID 1 would be used for the broadcast address, and host ID 0 would be the network itself, leaving no room for actual hosts. That’s why the maximum network ID size is 30 bits.
    * Because the network ID portion of a subnet mask is always composed of consecutive bits set to 1, only eight values are possible for each octet of a subnet mask: 0, 128, 192, 224, 248, 252, 254, and 255.
    * A subnet address can’t be all zeros or all ones. Thus, the number of unique subnet addresses is two less than two raised to the number of subnet address bits. For example, with three subnet address bits, six unique subnet addresses are possible (2^3 – 2 = 6). This implies that you must have at least two subnet bits. (If a single-bit subnet mask were allowed, it would violate the “can’t be all zeros or all ones” rule because the only two allowed values would be 0 or 1.)

Find a valid IP range for a given CIDR:

192.168.1.100
IP address: 11000000 10101000 00000001 01100100

Logical AND

Subnet mask: 11111111 11111111 11111111 11110000 (255.255.240.0)

Equals

Network ID: 11000000 10101000 00000001 01100000

192.168.1.96

Now look at the prefix (192) to determine the number of allowed IP addresses (14 in this case). They will start at the IP right after the Network ID (192.168.1.97)

# Private Network IPs

10.0.0.0/8                 10.0.0.1–10.255.255.254

172.16.0.0/12            172.16.1.1–172.31.255.254

192.168.0.0/16         192.168.0.1–192.168.255.254

# NAT

Network address translation is used by many firewalls to hide the host address from the outside world.

# Routing

Routing is for:
    * connecting to the Internet
    * connecting remote offices to each other via the Internet
    * managing traffic in extremely large networks such as large campuses, huge office buildings, or the Internet itself.

## Residential (consumer-grade)

A residential gateway typically includes five distinct components, all bundled into one neat package:
    * A router, used to connect your private network to your ISP’s network
    * A small switch, typically providing from three to eight ports to connect wired devices such as computers and printers
    * A wireless access point (WAP) to connect wireless devices such as laptops or smartphones
    * A firewall to provide protection from intruders seeking to compromise your network
    * A DHCP server to provide IP addresses for the computers and other devices on your network

Demark (demarcation point): a virtual line which divides the responsibility between the ISP and the customer.

## Routing table

The first rule that matches destination IP in the table is executed.

255.255.255.255 subnet mask means that the destination is a specific IP address, not a network

network IP address 0.0.0.0 with no subnet mask (eg. SM 0.0.0.0) means that all packets that aren’t caught by any of the other rules are forwarded out to the ISP’s gateway router on the external interface.

# DHCP
:dhcp:

Common options configured by DHCP:
    * configure IP addresses for hosts on the network
    * configure their Subnet Masks
    * The router address, also known as the Default Gateway address
    * The expiration time for the confguration information
    * Domain name
    * Domain Name Server (DNS) server address
    * Windows Internet Name Service (WINS) server address

Most networks can use file server as dhcp server. But router is a better option, since it doesn't need to be powered down.

Lease is the term used by DHCP to indicate that an IP address has been temporarily given out to a particular computer or other device.

Lease length considerations:
    * The more stable your network, the longer the lease duration can safely exist. If you only periodically add new computers to the network or replace existing computers, you can safely increase the lease duration past eight days.
    * The more volatile the network, the shorter the lease duration should be. For example, a wireless network in a university library is used by students who bring their laptop computers into the library to work for a few hours at a time. For this network, a duration such as one hour may be appropriate.
    * Either way, don't make leases infinite

Client attempts renewing lease half-way through the lease length. To renew manually launch ipconfig /renew

## APIPA

:apipa:arpa:

Automatic Private IP Addressing is used by the client computer, when IP address isn't available from dhcp server. Watch out for the 169.254.x.x  range

How DHCP works:

    1. When a host computer starts up, the DHCP client software sends a special broadcast packet, known as a DHCP Discover message.
    2. This message uses the subnet’s broadcast address (all host ID bits set to one) as the destination address and 0.0.0.0 (since it doesn't have any IP yet) as the source address.
    3. The DHCP server receives the broadcast DHCP Discover message and responds by sending a DHCP Offer message (offer is not final, until accepted by the client), which includes a shiny new IP, to the broadcast IP (that's the only way new client can receive it). If client doesn't receive the response, it will re-try the request
    4. The client receives the DHCP Offer message and sends back a message known as a DHCP Request message. The IP is not finalized until DHCP grants it
    5. When the server receives the DHCP Request message, it marks the IP address as assigned to the client and broadcasts a DHCP Ack message
    6. When the client receives the DHCP Ack message, it configures its TCP/IP stack by using the address it accepted from the server.

Scope is a range of IP addresses that a DHCP server is configured to distribute. You must create a scope before you can enable a DHCP server. When you create a scope, you can provide it with the following properties:
    * A scope name, which helps you to identify the scope and its purpose
    * A scope description, which lets you provide additional details about the scope and its purpose
    * A starting IP address for the scope
    * An ending IP address for the scope
    * A subnet mask for the scope. You can specify the subnet mask with dotted-decimal notation or with network pre x notation.
    * One or more ranges of excluded addresses. These addresses won’t be assigned to clients. For more information, see the section “Feeling excluded?” later in this chapter.
    * One or more reserved addresses. These are addresses that will always be assigned to particular host devices. For more information, see the section “Reservations suggested” later in this chapter.
    * The lease duration, which indicates how long the host will be allowed to use the IP address. The client will attempt to renew the lease when half of the lease duration has elapsed. For example, if you specify a lease duration of eight days, the client will attempt to renew the lease after four days. This allows the host plenty of time to renew the lease before the address is reassigned to some other host.
    * The router address for the subnet. This value is also known as the Default Gateway address.
    * The domain name and the IP address of the network’s DNS servers and WINS servers.

Here are a few reasons for excluding IP addresses from a scope:
    * The computer that runs the DHCP service itself must usually have a static IP address assignment. As a result, the address of the DHCP server should be listed as an exclusion.
    * Some hosts, such as a server or a printer, may need to have a predictable IP address. In that case, the host will require a static IP address. By excluding its IP address from the scope, you can prevent that address from being assigned to any other host on the network.

Configuring Static IP on the host pitfalls:
    * TCP/IP configuration supplies more than just the IP address. If you use static configuration, you must manually specify the subnet mask, the Default Gateway address, the DNS server address, and other configuration information required by the host. If this information changes, you have to change it not only at the DHCP server, but also at each host that you configured statically.
    * You must remember to exclude the static IP address from the DHCP server’s scope. Otherwise, the DHCP server won’t know about the static address and may assign it to another host. Then, you’ll have two hosts with the same address on your network.

Better way to configure static IP is by making DHCP reservation. You'd need to relate it to the MAC address of the host (ipconfig /all). That way when the particular host requests an IP, it will get that IP from DHCP.

BootP (Bootstrap Protocol) can provide (along with the IP) a boot image to a disk less workstation. Most dhcp servers support it. But it's not used much anymore.

# DNS
:dns:fqdn:hosts-file:

Domain name server provides names for ip addresses.

Only 63 alphanumeric and hyphens are allowed.

FQDN fully qualified domain name includes the dot at the end, which represents the root.

Top level domain categories:
    * generic
    * Geographic
    * Reverse lookups

Hosts file:
    * The Hosts file is not dead. For small networks, a Hosts file may still be the easiest way to provide name resolution for the network’s computers. In addition, a Hosts file can coexist with DNS. The Hosts file is always checked before DNS is used, so you can even use a Hosts le to override DNS if you want. (Win callback home overrides it on system level)
    * The Hosts file is the precursor to DNS. DNS was devised to circumvent the limitations of the Hosts file. You’ll be in a better position to appreciate the benefits of DNS when you understand how the Hosts file works.

Hosts file location:
    * Windows:   c:\windows\system32\drivers\etc
    * Linux:         /etc/hosts

Aliases in hosts file

"s1" is an alias, this host can be accessed by simply using s1

192.168.168.201 server1.LoweWriter.com s1

DNS Zones

You can set up your own DNS server, which will provide DNS management for your domain name. You can set up separate servers to handle multiple zones, to distribute the load.

    Primary zone is where all of the changes are made
    Secondary zone always obtains the configurations from the primary

