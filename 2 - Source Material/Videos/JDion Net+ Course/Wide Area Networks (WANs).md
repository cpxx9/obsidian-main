Tags: [[networking]] [[network-media]] [[physical-networking]]

# Wide Area Networks (WANs)
### About
###### Author: *Jason Dion*
###### URL: *https://udemy.com/course/comptia-network-009/learn/lecture/42186186#overview*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
##### Connections
###### Fiber Optic
FTTH (Fiber to the Home) - Fastest
- Fiber goes directly into residence/office
FTTB (Building/Basement) - Fast
- Fiber goes to a buildings main communication room or basement, copper there to units or offices within the building
FTTC (to the Curb/Cabinet) Slow
- Fiber runs to nearby curbside or cabinet, then copper to the home
FTTN (Node/Neighborhood) Slowest
- Fiber goes to central point in a neighborhood, copper from there to homes
###### Cable (DOCSIS)
- use the same lines that cable television used
- easy and cheap to install as many homes already have it
HFC
- high capacity highway that carries very large amounts of data using fiber and coaxial cable
- high speed, long distance
- fiber from ISP root facility to distribution facility
- coaxial from there to homes
DOCSIS
- standard of how data is transmitted over a hybrid fiber-coax network
- upstream
	- 5-42 MHz
- Downstream
	- 50-860 MHz
- means higher download speeds than uploads
###### Digital Subscriber Line (DSL)
- transmit data over telephone networks
- easy and cheap to install as many homes already have it
ADSL (Asymmetrical)
- different download and upload speeds
SDSL (Symmetrical)
- same download and upload speeds
VDSL (Very High Bit-Rate)
- very high speeds with downloads reaching 50 Mbps and uploads 10 Mbps
- only available if 4000 feet of less from DSLAM
	- DSLAM is the point of presence that is owned by your telephone company
###### Satellite
- uses satellites in orbit
- available pretty much anywhere, as long as you have vision to the sky
- remote locations, moving offices (trailers, RVs)
- Geo-Synchronous Satellites
	- 22,000 miles above the earth
	- only need about 6 to cover the entire earth
	- very high latency, almost 500ms just from distance travel speeds
- Low Earth Orbit Satellites
	- Starlink
	- only about 500 miles in the air
	- Need thousands to cover the earth
	- 25ms latency
###### Cellular

|  GENERATION  |  FREQUENCY  |          SPEED           |
| :----------: | :---------: | :----------------------: |
|      1G      |   30 KHz    |          2Kbps           |
|      2G      |  1800 MHz   |       14.4-64 Kbps       |
|      3G      |  1.6-2 GHz  |    144 Kbps - 2 Mbps     |
|      4G      |   2-8 GHz   |    100 Mbps - 1 Gbps     |
| 5G Low-Band  | 600-850 MHz |       30-250 Mbps        |
| 5G Mid-Band  | 2.5-3.7 GHz |       10-900 Mbps        |
| 5G High-Band |  25-39 GHz  | Extremely fast (in Gbps) |
GSM (Global System for Mobile Communications)
- global cellular technology
- converts voice data to digital data
- device is given a channel and time slot
	- calls can be combined with several other users' 
- new GSM versions use a lot of CDMA features
CDMA
- every calls data is encoded with a key
- all calls' data can be transferred over the same channel
- receiver has the key for your specific call data, does not get others'
Both are pretty much the same now adays in terms of speed/reliability
GSM is more widely supported across the globe
###### Microwave
- Beam of radio waves in microwave frequency range to transmit data between 2 fixed locations
- Satellite dish needed on each point
- very high speeds over long distances (~40 miles)
	- distance only degraded due to curve in Earth
- expensive, and complex to install
- Not as popular nowadays that 4G and 5G cellular are out
	- Cellular is much easier and cheaper to install
###### Leased Line
- Direct physical cable from one point to another
- fixed bandwidth and symmetric data connection that is exclusively reserved
- some of the highest speed, reliability, and security
- very expensive
###### MPLS (Multiprotocol Label Switching)
- helps reduce router operations
- versatile
	- all traffic is treated the same, no matter the protocol
- used by ISPs
- network of MPLS enabled routers somewhere on the backbone
- Ingress - Entry point of MPLS network router
- Egress - exit point of MPLS network router
When Traffic Comes into the MPLS network
- Label Assignment
	- Ingress router assigns the packet a label, short fixed length ID
	- encapsulates the packet's forwarding info
- Label Switching
	- as packet travels through the MPLS network
	- Core routers look at the label to make forwarding decisions
	- forwarding tables based on Labels
- Label Removal
	- Egress router removes the label, and forwarded based on original IP header