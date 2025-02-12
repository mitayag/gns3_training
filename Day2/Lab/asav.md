---

# **GNS3 Lab: ASAv Firewall Allowing All Traffic**

This tutorial guides you through setting up a simple lab in GNS3 with an ASAv (Cisco Adaptive Security Appliance Virtual) as a firewall. In this configuration, all traffic will be allowed to ensure full connectivity between clients and the internet. This setup is ideal for learning or troubleshooting purposes.

---

## **Step 1: Set Up the GNS3 Topology**

1. **Add Devices to the Workspace:**
   - Drag an **ASAv** device from the GNS3 device list onto the workspace.
   - Add a **Cloud** device (NAT Cloud) to provide internet connectivity.
   - Add a **Switch** device to connect multiple clients.
   - Add two **VPCs** (Virtual PCs) to act as client machines.

2. **Connect the Devices:**
   - Connect one interface of the **ASAv** (e.g., `GigabitEthernet0/0`) to the **Cloud** (NAT Cloud).
   - Connect another interface of the **ASAv** (e.g., `GigabitEthernet0/1`) to the **Switch**.
   - Connect both **VPCs** to the **Switch**.

---

## **Step 2: Configure the ASAv Firewall**

### **Basic Configuration on ASAv**

1. **Access the ASAv Console:**
   - Open the console for the ASAv by right-clicking on the ASAv in GNS3 and selecting "Console."

2. **Enter Global Configuration Mode:**
   ```bash
   enable
   configure terminal
   ```

3. **Configure Interfaces:**

   - **GigabitEthernet0/0 (Outside Interface):**
     This interface connects to the NAT Cloud (Internet).
     ```bash
     interface GigabitEthernet0/0
     nameif outside
     security-level 0
     ip address dhcp
     no shutdown
     exit
     ```

   - **GigabitEthernet0/1 (Inside Interface):**
     This interface connects to the internal network (clients).
     ```bash
     interface GigabitEthernet0/1
     nameif inside
     security-level 100
     ip address 192.168.1.1 255.255.255.0
     no shutdown
     exit
     ```

4. **Enable NAT for Internet Access:**
   - Configure NAT to allow internal clients to access the internet.
     ```bash
     object network INTERNAL_NETWORK
     subnet 192.168.1.0 255.255.255.0

     nat (inside,outside) dynamic interface
     exit
     ```

5. **Allow Management via ASDM:**
   - Enable HTTPS for ASDM access.
     ```bash
     http server enable
     http 192.168.1.0 255.255.255.0 inside
     ```

6. **Create an ACL to Allow All Traffic:**
   - Create an ACL named `ALLOW_ALL` that permits all IP traffic:
     ```bash
     access-list ALLOW_ALL extended permit ip any any
     ```

   - Apply the ACL to the `inside` interface in the inbound direction:
     ```bash
     access-group ALLOW_ALL in interface inside
     ```

7. **Save the Configuration:**
   ```bash
   write memory
   ```

---

## **Step 3: Configure Client PCs (VPCs)**

1. **Assign IP Addresses to VPCs:**
   - For **VPC1**:
     ```bash
     ip 192.168.1.10 255.255.255.0 192.168.1.1
     save
     ```
   - For **VPC2**:
     ```bash
     ip 192.168.1.20 255.255.255.0 192.168.1.1
     save
     ```

2. **Test Connectivity:**
   - From each VPC, try pinging the ASAv's inside interface (`192.168.1.1`):
     ```bash
     ping 192.168.1.1
     ```

---

## **Step 4: Verify Internet Connectivity**

1. **Ping an External IP Address:**
   - From the VPCs, try pinging an external IP address (e.g., Google's DNS server `8.8.8.8`):
     ```bash
     ping 8.8.8.8
     ```

   - If this succeeds, the clients have internet access.

2. **Test DNS Resolution:**
   - Try resolving a domain name (e.g., `google.com`):
     ```bash
     nslookup google.com
     ```

   - If this fails, configure DNS servers manually:
     ```bash
     ip dns server-address 8.8.8.8
     ```

---

## **Step 5: Access ASDM for Management**

1. **Open ASDM:**
   - On your local machine, open a web browser and navigate to `https://192.168.1.1`.
   - Log in using the default credentials:
     - Username: `admin`
     - Password: `Admin123` (or whatever password you set during initial configuration).

2. **Manage the ASAv via ASDM:**
   - Use ASDM to further configure the firewall, monitor traffic, and manage policies.

---

## **Step 6: Troubleshooting**

If the clients cannot access the internet, follow these steps:

1. **Verify NAT Translation:**
   - Check if NAT translations are occurring:
     ```bash
     show xlate
     ```

   - Look for entries showing translations from the client's private IP address (`192.168.1.x`) to the outside interface's public IP address.

2. **Check Default Route:**
   - Ensure the ASAv has a default route pointing to the NAT Cloud's gateway:
     ```bash
     show route
     ```

   - If missing, add the default route:
     ```bash
     route outside 0.0.0.0 0.0.0.0 <gateway_ip>
     ```

3. **Debug Traffic Flow:**
   - Use the `packet-tracer` command to simulate traffic flow:
     ```bash
     packet-tracer input inside tcp 192.168.1.10 12345 8.8.8.8 80 detailed
     ```

---

## **Summary of Key Points**

- **Topology:** ASAv connected to NAT Cloud (outside) and clients via a switch (inside).
- **NAT:** Dynamic NAT translates internal IPs to the outside interface's public IP.
- **ACL:** An ACL (`ALLOW_ALL`) is configured to permit all traffic.
- **Management:** ASDM access is enabled for GUI-based management.
- **Troubleshooting:** Use `show xlate`, `show route`, and `packet-tracer` to debug connectivity issues.

