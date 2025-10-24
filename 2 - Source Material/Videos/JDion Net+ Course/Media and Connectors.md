Tags: [[networking]][[network-media]]

# Media and Connectors
### About
###### Author: *Jason Dion*
###### URL: *https://udemy.com/course/comptia-network-009/learn/lecture/42185668#overview*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
#### Copper Media
###### Twisted Pair Cable
CAT 5
- 100Mbps
- 100 meters
- 100 MHz frequency
- 100 BASE-T (Fast Ethernet)
CAT 5e
- 1000Mbps/1Gbps
- 100 meters
- 100 MHz frequency
- 1000 BASE-T (Gigabit Ethernet)
CAT 6
- 1/10Gbps
- 100/55 Meters
- 250 MHz frequency
- 1000 BASE-T (Gigabit Ethernet) / 10G BASE-T (10-Gigabit Ethernet)
CAT 6a
- 10Gbps
- 100 Meters
- 500 MHz frequency
- 10G BASE-T (10-Gigabit Ethernet)
CAT 7
- 10Gbps
- 100 Meters
- 600 MHz frequency
- 10G BASE-T (10-Gigabit Ethernet)
CAT 8
- 40Gbps
- 30 Meters
- 2000 MHz frequency / 2 GHz
###### Coaxial (Coax) Cable
- RG-9
	- older used for cable modems or long distance high speed connections
	- 1Gbps at 300 meters
- DAC
	- Direct Attach Copper
	- Active
		- 100Gbps at 15 meters or less
	- Passive
		- 100Gbps at 7 meters or less
	- 10/40/100 Gbps
- Twinaxial
	- often a component of a DAC
	- two cables run in parallel
	- less EMI than twisted pair cables
###### Plenum Cables
- Fire retardant
- Used in plenum spaces

##### Copper Media Connections
- wiring kits are pretty cheap $10-15
RJ-11 (Registered Jack 11)
- 6 pin connector used for phone lines
- carries less data as it only uses 6 of 8 wires in cable
- clip in
RJ-45 (Registered Jack 45)
- 8 pin connector used for ethernet cables (cat5e-8)
- uses all 8 wires in cable
- clip in
F-type RG-X (Radio Guide X (59 or 6))
- used for coax cables
- 59 is older, slower, not used
- screw in
BNC (Bayonet Neil-Concelman)
- used for coax cables
- higher speeds/bandwidth/stability than F-type
- push and twist in
- Also called British Naval Connector
#### Fiber Media
Single-Mode
- core 8-10 microns in diameter (hair is 17-180)
- can go for hundreds of miles
- 10-100 Gbps
- yellow jacket
- expensive
Multi-Mode
- core is 50-100 microns in diameter
- can go for about 2 kilometers
- 10-100 Gbps
- blue/orange jacket
- cheaper than single-mode
##### Fiber Media Connections
- wiring kits are expensive $150-250
SC (Subscriber Connector)
- Push Pull
- square shape
- precise, minimal signal loss, durable, easy to use
- Stick Click
- used for single mode
LC (Lucent Connector)
- Push Pull 
- smaller form factor than SC, very similar square shape
- precise, minimal signal loss, slightly harder to use being smaller
- often connectors are bound together (Love Connector)
- used when space is restricted
ST (Straight Tip)
- Twist-lock 
- round shape
- very robust
- Stick and Twist
- used in environments with high movement/vibration or outdoors
MTRJ (Mechanical Transfer-Registered Jack)
- transmit and receive fibers in same connector
- small rectangular design
- used when space is restricted (fiber switches)
MPO (Multi-Fiber Push On)
- designed to have multiple fibers in a single connector
- increases capacity and flexibility of a fiber network
- used in data-centers, high speed networks (backbones, interconnections)
###### Polishes
- back reflection causes signal degradation in fiber cables
	- transmitted light comes back into the transmitter
- different polishes help minimize this back reflection
PC (Physical Contact)
- least effective reduction in back reflection
- cheapest
UPC (Ultra Physical Contact)
- updated PC
- good balance of performance and cost
APC (Angled Physical Contact)
- lowest back reflection
- most expensive
#### Transceivers
- L1 devices that can transmit and receive data
- can convert data from one protocol into another
	- ethernet to fiber channel, etc.
- or one type into another
- ethernet to ethernet with fiber in the middle, etc.
SFP (Small Form Factor Pluggable)
- 4.25 Gbps
- single channel
- older
SFP+ (Small Form Factor Pluggable Plus)
- 16 Gbps
- single channel
- Updated SFP
QSFP (Quad Small Form Factor Pluggable)
- 10 Gbps
- quad channel
QSFP+ (Small Form Factor Pluggable Plus)
- 40 Gbps
- quad channel
QSFP28 (Small Form Factor Pluggable) 
- 100 Gbps
- quad channel
QSFP56 (Small Form Factor Pluggable)
- 200 Gbps
- quad channel