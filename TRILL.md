# **TRILL**

**TRILL ("TRansparent Interconnection of Lots of Links")** is an IETF Standard implemented by devices called RBridges (routing bridges) or TRILL Switches. TRILL combines techniques from bridging and routing and is the application of link state routing to the VLAN-aware customer-bridging problem. RBridges are compatible with and can incrementally replace previous IEEE 802.1 customer bridges. They are also compatible with IPv4 and IPv6 routers and end nodes. They are invisible to current IP routers and, like routers, RBridges terminate the bridge spanning tree protocol.

## **General overview**

TRILL switches (RBridges) run a link state protocol amongst themselves. A link state protocol is one in which connectivity is broadcast to all the RBridges, so that each RBridge knows about all the other RBridges, and the connectivity between them. This gives RBridges enough information to compute pair-wise optimal paths for unicast, and calculate distribution trees for delivery of frames either to destinations whose location is unknown or to multicast or broadcast groups. The link state routing protocol used is IS-IS because:

- it runs directly over Layer 2, so it can be run without configuration (no IP addresses need to be assigned)
- it is easy to extend by defining new TLV (type-length-value) data elements and sub-elements for carrying TRILL information.

To mitigate temporary loop issues, RBridges forward based on a header with a hop count. RBridges also specify the next hop RBridge as the frame destination when forwarding unicast frames across a shared media link, which avoids spawning additional copies of frames during a temporary loop. A reverse path forwarding check and other checks are performed on multi-destination frames to further control potentially looping traffic.

The first RBridge that a unicast frame encounters in a campus, RB1, encapsulates the received frame with a TRILL header that specifies the last RBridge, RB2, where the frame is decapsulated. RB1 is known as the "ingress RBridge" and RB2 is known as the "egress RBridge". To save room in the TRILL header and simplify forwarding lookups, a dynamic nickname acquisition protocol is run among the RBridges to select two-octet nicknames for RBridges, unique within the campus, which are an abbreviation for the six-octet IS-IS system ID of the RBridge. The two-octet nicknames are used to specify the ingress and egress RBridges in the TRILL header.

The TRILL header consists of six octets: the first two octets include a six bit decrementing hop count, plus flags; the next two octets contain the egress RBridge nickname; the final two octets contain the ingress RBridge nickname. For multi-destination frames, the "egress RBridge nickname" specifies a distribution tree for the frame, where the (nick)named RBridge is the root of the distribution tree. The ingress RBridge selects which distribution tree the frame should travel along.

Even though RBridges are transparent to Layer 3 devices, and all the links interconnected by RBridges appear to Layer 3 devices to be a single link, RBridges act as link routers in the sense that, in the forwarding of a frame by a transit RBridge, the outer Layer 2 header is replaced at each hop with an appropriate Layer 2 header for the next hop, and the hop count is decreased. Despite these modifications of the outer Layer 2 header and the hop count in the TRILL Header, the original encapsulated frame is preserved, including the original frame's VLAN tag.

Multipathing of multi-destination frames through alternative distribution tree roots and ECMP (Equal Cost MultiPath) of unicast frames are supported. Networks with a more mesh-like structure will benefit to a greater extent from the multipathing and optimal paths provided by TRILL than will networks with a more tree-like structure.
	
## **TRILL links**
  
From the point of view of TRILL, a link can be any of a wide variety of link technologies, including IEEE 802.3 (Ethernet), PPP (Point to Point Protocol), or a Pseudo-wire Ethernet links between RBridges can incorporate IEEE customer or provider 802.1 bridges. In other words, an arbitrary bridged LAN appears to an RBridge as a multi-access link.

It is essential that only one RBridge act as the ingress RBridge for any given native frame and TRILL has an Appointed Forwarder mechanism to assure this. TRILL does allow load splitting of this duty on a link based on VLAN, so that only one RBridge on each link encapsulates and decapsulates native frames for each VLAN.

## **RBridge ports**
  
RBridge ports can compatibly implement a wide variety of existing and proposed link level and IEEE 802.1 port level protocols including PAUSE (IEEE 802.3 Annex 31B), the Link Layer Discovery Protocol (IEEE 802.1AB), link aggregation (IEEE 802.1AX), MAC security (IEEE 802.1AE), or port based access control (IEEE 802.1X). This is because RBridges are layered above the IEEE 802.1 EISS (Extended Internal Sublayer Service) with the exception that an RBridge port handles spanning tree and VLAN registration PDUs differently.

## **Proprietary implementations**
  
Cisco FabricPath is a proprietary implementation of TRILL that utilizes the TRILL control plane (including IS-IS for Layer 2), but a non-interoperable data plane. Brocade Virtual Cluster Switching, uses the TRILL data plane but a proprietary control plane and so is not interoperable with standards conformant TRILL.

## **Limitations**
  
- TRILL uses two different mechanisms to forward packets, making it difficult to know the path of packets.
- TRILL is susceptible to out-of-order packets when the MAC state transitions from unknown to known for Multicast, broadcast and Unknown packets.

	
## **Competitors**
  
The IEEE 802.1aq standard (Shortest Path Bridging – SPB) is considered the major competitor of TRILL. As one 2011 book noted,  "the evaluation of relative merits and difference of the two standards proposals is currently a hotly debated topic in the networking industry."
	
## **Product support**
  
- HP 5700, 5900, 5920, 5930, 7900, 11900, 12500, 12900 Switch Series
- Huawei Cloud Engine 5800, 6800, 7800, and 12800 Switches
- Enterasys / Extreme Networks S-Series Switch Range
- Ruijie Networks RG-S6220, RG-S12000, and RG-N18000 Series

## **Links** 

- https://en.wikipedia.org/wiki/TRILL_(computing)
- http://www.cisco.com/c/en/us/about/press/internet-protocol-journal/back-issues/table-contents-53/143-trill.html
- http://blog.ine.com/tag/trill/
