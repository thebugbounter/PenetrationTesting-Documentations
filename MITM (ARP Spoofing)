# Network Probing and ARP Spoofing Configuration

This guide outlines the steps for setting up network probing, ARP spoofing, and packet sniffing on a local network. The configuration will allow for sending probe packets, performing a Man-in-the-Middle (MITM) attack through ARP spoofing, and capturing network traffic from selected targets.
### 1. Start Bettercap:

**Command:**
```
bettercap
```

### 2. Enable Network Probing

**Command:**
```
net.probe on
```
**Description:**
This command activates the network probing feature, which sends various types of probe packets to identify active devices and network configurations.

### 3. Configure ARP Spoofing for Full Duplex

**Command:**
```
set arp.spoof.fullduplex true
```

**Description:**
Enables full-duplex ARP spoofing. This mode allows spoofing ARP replies to both the target and the gateway, facilitating a MITM attack. In this setup, crafted ARP packets are sent to trick selected hosts into sending their traffic through the attacker's machine.

### 4. Set ARP Spoofing Targets

**Command:**
```
set arp.spoof.targets <Target IP>
```

**Description:**
Specifies the IP address of the target device to be spoofed. Replace `<Target IP>` with the actual IP address of the victim device you want to intercept.

### 5. Enable Local Packet Sniffing

**Command:**
```
set net.sniff.local true
```

**Description:**
Activates packet sniffing on the local network. This allows the attacker to capture and analyze data packets sent and received by the target devices.

### 6. Start ARP Spoofing

**Command:**
```
arp.spoof on
```
**Description:**
Begins the ARP spoofing process. This command sends forged ARP packets to the target and the gateway, redirecting the network traffic through the attacker's machine.

### 7. Start Packet Sniffing

**Command:**
```
net.sniff on
```
**Description:**
Initiates the packet sniffing process. With this command, the attacker can monitor and capture all traffic between the target device and the network.

