
# Content of the Markdown file
markdown_content = """# Network Topology with VLANs and Trunking

This document outlines the configuration of a simple network topology using two Cisco Layer 2 switches, VLANs, trunking, and end devices.

---

## **IP Address Assignment and VLAN Configuration**

### **End Device IP Address Assignments**
| **Device** | **Interface** | **IP Address**     | **Subnet Mask**     | **VLAN**                  |
|------------|---------------|--------------------|---------------------|---------------------------|
| **PC1**    | `eth0`        | `192.168.10.2`    | `255.255.255.0`     | **VLAN 10 (Sales)**       |
| **PC2**    | `eth0`        | `192.168.20.2`    | `255.255.255.0`     | **VLAN 20 (Engineering)** |
| **PC3**    | `eth0`        | `192.168.10.3`    | `255.255.255.0`     | **VLAN 10 (Sales)**       |
| **PC4**    | `eth0`        | `192.168.20.3`    | `255.255.255.0`     | **VLAN 20 (Engineering)** |

---

### **Switches: CiscoL2SW1 Configuration**
| **Interface**         | **IP Address**       | **Subnet Mask**     | **VLAN**                  | **Role**                 |
|-----------------------|----------------------|---------------------|---------------------------|--------------------------|
| **VLAN 1 (Management)** | `192.168.1.1`      | `255.255.255.0`     | **VLAN 1 (Default)**      | Management Interface     |
| **e0/1**              | Access Port         | -                   | **VLAN 10 (Sales)**       | Connected to PC1         |
| **e0/2**              | Access Port         | -                   | **VLAN 20 (Engineering)** | Connected to PC2         |
| **e0/0**              | Trunk Port          | -                   | **VLAN 10, 20**           | Trunk to CiscoL2SW2     |

---

### **Switches: CiscoL2SW2 Configuration**
| **Interface**         | **IP Address**       | **Subnet Mask**     | **VLAN**                  | **Role**                 |
|-----------------------|----------------------|---------------------|---------------------------|--------------------------|
| **VLAN 1 (Management)** | `192.168.1.2`      | `255.255.255.0`     | **VLAN 1 (Default)**      | Management Interface     |
| **e0/1**              | Access Port         | -                   | **VLAN 10 (Sales)**       | Connected to PC3         |
| **e0/2**              | Access Port         | -                   | **VLAN 20 (Engineering)** | Connected to PC4         |
| **e0/0**              | Trunk Port          | -                   | **VLAN 10, 20**           | Trunk to CiscoL2SW1     |

---

## **Configuration Details**

### **CiscoL2SW1 Configuration**

```bash
enable
configure terminal

! Create VLANs
vlan 10
 name Sales
exit

vlan 20
 name Engineering
exit

! Configure Access Ports
interface Ethernet0/1
 switchport mode access
 switchport access vlan 10
exit

interface Ethernet0/2
 switchport mode access
 switchport access vlan 20
exit

! Configure Trunk Port
interface Ethernet0/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
exit

! Configure Management IP for VLAN 1
interface Vlan1
 ip address 192.168.1.1 255.255.255.0
 no shutdown
exit

! Save Configuration
write memory
```


### **CiscoL2SW2 Configuration**

```bash
enable
configure terminal

! Create VLANs
vlan 10
 name Sales
exit

vlan 20
 name Engineering
exit

! Configure Access Ports
interface Ethernet0/1
 switchport mode access
 switchport access vlan 10
exit

interface Ethernet0/2
 switchport mode access
 switchport access vlan 20
exit

! Configure Trunk Port
interface Ethernet0/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
exit

! Configure Management IP for VLAN 1
interface Vlan1
 ip address 192.168.1.2 255.255.255.0
 no shutdown
exit

! Save Configuration
write memory
```





