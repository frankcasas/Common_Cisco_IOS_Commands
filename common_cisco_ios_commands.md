### **Initial System & Management Configuration**
| Command | Configuration Mode | Purpose |
| :--- | :--- | :--- |
| **`enable`** | User Exec | Transitions from User Exec mode to Privileged Exec mode. |
| **`configure terminal`** | Privileged Exec | Transitions from Privileged Exec mode to Global Configuration mode. |
| **`hostname [name]`** | Global Config | Assigns a unique name to the network device. |
| **`clock set [hh:mm:ss] [month] [day] [year]`** | Privileged Exec | Manually updates the system clock. |
| **`service password-encryption`** | Global Config | Encrypts all existing and future plaintext passwords in the configuration with a weak Type 7 hash. |
| **`service timestamps log datetime msec`** | Global Config | Configures log messages to include dates and times with millisecond precision. |
| **`service sequence-numbers`** | Global Config | Adds sequence numbers to syslog messages for easier tracking. |
| **`banner motd [delimiter] [message] [delimiter]`** | Global Config | Displays a "Message of the Day" legal warning to users connecting to the device. |
| **`copy running-config startup-config`** | Privileged Exec | Saves the current configuration in RAM to the non-volatile NVRAM. |
| **`reload`** | Privileged Exec | Reboots the network device. |
| **`no ip domain-lookup`** | Global Config | Prevents the router from attempting to resolve misspelled commands as DNS hostnames. |
| **`description [text]`** | Interface Config | Adds a descriptive label to an interface to identify its purpose. |
| **`shutdown`** | Interface Config | Administratively disables a physical or logical interface. |
| **`no shutdown`** | Interface Config | Enables a previously disabled interface. |

---

### **Security, AAA, & Remote Access**
| Command | Configuration Mode | Purpose |
| :--- | :--- | :--- |
| **`enable secret [password]`** | Global Config | Sets a secure, MD5-hashed password for entering Privileged Exec mode. |
| **`enable algorithm-type scrypt secret [password]`** | Global Config | Uses the more secure SCRYPT (Type 9) hashing algorithm for the enable password. |
| **`username [name] secret [password]`** | Global Config | Creates a local user account with a secure hashed password. |
| **`aaa new-model`** | Global Config | Enables the Authentication, Authorization, and Accounting (AAA) framework on the device. |
| **`aaa authentication login [list] group [tacacs+/radius]`** | Global Config | Defines a method list for user login using a remote security server. |
| **`line con 0`** | Global Config | Enters configuration mode for the physical console port. |
| **`line vty 0 15`** | Global Config | Enters configuration mode for Virtual Terminal lines (remote access). |
| **`login local`** | Line Config | Configures the line to use the local username database for authentication. |
| **`transport input [ssh/telnet/none/all]`** | Line Config | Specifies which protocols are allowed to connect to the VTY lines. |
| **`exec-timeout [minutes] [seconds]`** | Line Config | Sets the interval that the device waits for user input before disconnecting a session. |
| **`access-class [acl] in`** | Line Config | Restricts remote access to the VTY lines based on an Access Control List. |
| **`crypto key generate rsa`** | Global Config | Generates the RSA key pairs required to enable SSH. |
| **`ip domain-name [name]`** | Global Config | Sets the DNS domain name required for RSA key generation. |
| **`ip ssh version 2`** | Global Config | Forces the device to use the more secure SSH version 2. |
| **`login block-for [sec] attempts [count] within [sec]`** | Global Config | Implements brute-force protection by blocking login attempts after failures. |

---

### **VLANs, Trunking, & EtherChannel**
| Command | Configuration Mode | Purpose |
| :--- | :--- | :--- |
| **`vlan [id]`** | Global Config | Creates a VLAN and enters VLAN configuration mode. |
| **`name [text]`** | VLAN Config | Assigns a descriptive name to a specific VLAN. |
| **`switchport mode access`** | Interface Config | Sets the interface as a permanent access port for end devices. |
| **`switchport access vlan [id]`** | Interface Config | Assigns an access port to a specific VLAN. |
| **`switchport voice vlan [id]`** | Interface Config | Assigns an interface to a voice VLAN for IP phones. |
| **`switchport mode trunk`** | Interface Config | Configures the interface to act as a permanent 802.1Q trunk. |
| **`switchport trunk allowed vlan [ids]`** | Interface Config | Limits which VLANs are permitted to send traffic across a trunk link. |
| **`switchport trunk native vlan [id]`** | Interface Config | Sets the VLAN ID for untagged traffic on an 802.1Q trunk. |
| **`switchport nonegotiate`** | Interface Config | Disables Dynamic Trunking Protocol (DTP) on the interface. |
| **`channel-group [id] mode [active/passive/on]`** | Interface Config | Bundles physical interfaces into an EtherChannel using LACP or static configuration. |
| **`interface port-channel [id]`** | Global Config | Enters configuration mode for a logical EtherChannel interface. |

---

### **Layer 2 Security & STP**
| Command | Configuration Mode | Purpose |
| :--- | :--- | :--- |
| **`switchport port-security`** | Interface Config | Enables port security on an interface. |
| **`switchport port-security maximum [count]`** | Interface Config | Sets the limit for the number of MAC addresses allowed on a secure port. |
| **`switchport port-security mac-address sticky`** | Interface Config | Enables "sticky" learning to save learned MAC addresses into the running configuration. |
| **`switchport port-security violation [shutdown/restrict/protect]`** | Interface Config | Defines the action taken when a security violation occurs on the port. |
| **`ip dhcp snooping`** | Global Config | Enables DHCP snooping to prevent rogue DHCP servers. |
| **`ip dhcp snooping trust`** | Interface Config | Sets an interface as a trusted source for DHCP server messages. |
| **`ip arp inspection vlan [id]`** | Global Config | Enables Dynamic ARP Inspection (DAI) on a specific VLAN to prevent spoofing. |
| **`spanning-tree mode rapid-pvst`** | Global Config | Switches the spanning-tree mode to Rapid PVST+. |
| **`spanning-tree vlan [id] priority [value]`** | Global Config | Manually sets the bridge priority to influence root bridge election. |
| **`spanning-tree portfast`** | Interface Config | Enables PortFast on an edge port to allow it to transition to forwarding immediately. |
| **`spanning-tree bpduguard enable`** | Interface Config | Protects PortFast-enabled ports by disabling them if they receive a BPDU. |

---

### **IP Routing & OSPF**
| Command | Configuration Mode | Purpose |
| :--- | :--- | :--- |
| **`ip address [ip] [mask]`** | Interface Config | Assigns an IPv4 address to an interface. |
| **`ip route [network] [mask] [next-hop]`** | Global Config | Configures an IPv4 static route. |
| **`ip route 0.0.0.0 0.0.0.0 [next-hop]`** | Global Config | Configures a default static route (Gateway of Last Resort). |
| **`ipv6 unicast-routing`** | Global Config | Enables the router to forward IPv6 traffic. |
| **`ipv6 address [address/prefix]`** | Interface Config | Assigns an IPv6 global unicast address to an interface. |
| **`router ospf [process-id]`** | Global Config | Enables the OSPFv2 routing process. |
| **`router-id [id]`** | Router Config | Manually assigns a unique identifier to the OSPF process. |
| **`network [ip] [wildcard] area [id]`** | Router Config | Identifies which interfaces participate in OSPF and assigns them to an area. |
| **`passive-interface [interface]`** | Router Config | Prevents OSPF Hello packets from being sent out an interface. |
| **`default-information originate`** | Router Config | Propagates a default route to all other routers in the OSPF domain. |

---

### **IP Services (DHCP, NAT, NTP, SNMP, Syslog)**
| Command | Configuration Mode | Purpose |
| :--- | :--- | :--- |
| **`ip dhcp pool [name]`** | Global Config | Creates a DHCP address pool and enters DHCP configuration mode. |
| **`network [network-id] [mask]`** | DHCP Config | Defines the range of IP addresses to be distributed by the DHCP server. |
| **`default-router [ip]`** | DHCP Config | Sets the default gateway for DHCP clients. |
| **`ip dhcp excluded-address [start] [end]`** | Global Config | Reserves a range of addresses that the DHCP server will not assign to clients. |
| **`ip helper-address [ip]`** | Interface Config | Configures a DHCP relay agent to forward broadcasts to a remote DHCP server. |
| **`ip nat inside source static [local] [global]`** | Global Config | Configures a one-to-one static NAT mapping. |
| **`ip nat pool [name] [start] [end] netmask [mask]`** | Global Config | Defines a pool of public IP addresses for dynamic NAT or PAT. |
| **`ip nat inside source list [acl] interface [int] overload`** | Global Config | Configures Port Address Translation (PAT) using an ACL and an outside interface. |
| **`ntp server [ip]`** | Global Config | Synchronizes the system clock with an external NTP server. |
| **`ntp master [stratum]`** | Global Config | Configures the local router to act as an authoritative NTP time source. |
| **`logging host [ip]`** | Global Config | Sends syslog messages to a remote syslog server. |
| **`logging trap [severity]`** | Global Config | Filters which severity levels of syslog messages are sent to the remote host. |
| **`snmp-server community [string] [ro/rw]`** | Global Config | Sets the SNMP community string and access level (Read-Only or Read-Write). |

---

### **Access Control Lists (ACLs)**
| Command | Configuration Mode | Purpose |
| :--- | :--- | :--- |
| **`access-list [permit/deny] [source]`** | Global Config | Creates a numbered standard IPv4 ACL entry. |
| **`access-list [permit/deny] [protocol] [source] [dest] eq [port]`** | Global Config | Creates a numbered extended IPv4 ACL entry. |
| **`ip access-list standard [name]`** | Global Config | Creates a named standard ACL. |
| **`ip access-list extended [name]`** | Global Config | Creates a named extended ACL. |
| **`ip access-group [id/name] [in/out]`** | Interface Config | Applies an ACL to an interface to filter traffic in a specific direction. |
| **`remark [text]`** | ACL Config | Adds a comment/description to an ACL entry for documentation. |

---

### **Verification & Show Commands**
| Command | Configuration Mode | Purpose |
| :--- | :--- | :--- |
| **`show ip interface brief`** | Privileged Exec | Displays a summary of interface IP addresses and operational status. |
| **`show ip route`** | Privileged Exec | Displays the current IPv4 routing table. |
| **`show vlan brief`** | Privileged Exec | Lists all configured VLANs and their assigned ports. |
| **`show interface trunk`** | Privileged Exec | Shows active trunking interfaces and their allowed VLANs. |
| **`show mac address-table`** | Privileged Exec | Displays the MAC-to-port mappings in the CAM table. |
| **`show cdp neighbors`** | Privileged Exec | Lists directly connected Cisco devices. |
| **`show ip nat translations`** | Privileged Exec | Displays active NAT and PAT translation entries. |
| **`show standby`** | Privileged Exec | Displays the status and virtual IP information for HSRP. |
| **`ping [target]`** | Any Exec | Tests end-to-end IP connectivity. |
| **`traceroute [target]`** | Any Exec | Traces the hop-by-hop path to a destination. |
