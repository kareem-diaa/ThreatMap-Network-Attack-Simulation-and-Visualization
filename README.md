# README.md — THREAT_FINAL

````markdown
# THREAT_FINAL
## ThreatMap – Network Attack Simulation & Visualization

> Final Version Project Name: **THREAT_FINAL**

---

# Project Overview
THREAT_FINAL is the final version of a cybersecurity simulation and visualization project developed using Cisco Packet Tracer.

The project demonstrates how different cyberattacks affect a network environment and how multiple defensive mechanisms respond in real time.

The project simulates:
- DoS-style ICMP attacks
- Port scanning attacks
- MAC flooding attacks
- Rogue DHCP behavior

The project also demonstrates:
- ACL filtering
- Port Security
- DHCP Snooping
- OSPF routing
- Syslog monitoring
- Secure administrative access

---

# Objectives
- Simulate real-world cyberattacks
- Visualize attack impact on the network
- Demonstrate layered security defenses
- Maintain legitimate network connectivity
- Generate attack-response logging evidence

---

# Technologies Used
- Cisco Packet Tracer
- Cisco IOS CLI
- Syslog Server
- ACL Security Policies
- Port Security
- DHCP Snooping
- OSPF Routing

---

# Network Topology
The topology contains:
- Attacker Network
- Legitimate Client Network
- Protected Servers
- Core Switch
- ACL Router
- Syslog Server
- DHCP Services

The topology is designed to clearly visualize:
- Attack sources
- Defensive filtering points
- Logging locations
- Protected network zones

---

# Security Features

## 1. ACL-Based Protection
ACLs are configured on the router to:
- Block hostile ICMP traffic
- Block management port probing
- Allow legitimate traffic

### Protected Ports
- SSH (22)
- Telnet (23)
- RDP (3389)

---

## 2. Port Security
Switch Port Security is configured to:
- Allow only authorized MAC addresses
- Detect MAC flooding attempts
- Automatically shutdown compromised ports

---

## 3. DHCP Snooping
DHCP Snooping protects the network from:
- Rogue DHCP servers
- DHCP spoofing
- Unauthorized DHCP replies

---

## 4. OSPF Routing
OSPF is configured to:
- Enable communication between segmented networks
- Dynamically exchange routing information
- Maintain scalable routing architecture

---

## 5. Syslog Monitoring
The Syslog server records:
- Interface state changes
- Security-related events
- Configuration changes
- Router activity logs

---

# Attack Simulations

## 1. DoS-Style ICMP Attack
### Objective
Simulate repeated ICMP traffic from the attacker network.

### Expected Defense
- Router ACL blocks ICMP packets
- Protected servers remain unreachable
- ACL match counters increase

---

## 2. Port Scanning Attack
### Objective
Simulate probing of management services.

### Targeted Ports
- 22 (SSH)
- 23 (Telnet)
- 3389 (RDP)

### Expected Defense
- ACL denies access
- Connection attempts timeout
- Management services remain protected

---

## 3. MAC Flooding / Port Security Violation
### Objective
Trigger unauthorized MAC address behavior.

### Expected Defense
- Switch detects violation
- Interface enters Secure-shutdown state
- Port becomes err-disabled

---

## 4. Rogue DHCP Simulation
### Objective
Simulate unauthorized DHCP server behavior.

### Expected Defense
- DHCP Snooping blocks rogue DHCP replies
- Only trusted interfaces can forward DHCP responses

---

# ThreatMap Detailed Test Checklist

## 1. Router ACL Baseline Check

### Device
Router-ACL

### Commands
```bash
enable
show access-lists
show running-config
````

### Expected Result

* ACL ANTI-DOS exists
* ICMP blocking rules exist
* Ports 22, 23, and 3389 are blocked
* Syslog configuration is enabled

---

## 2. Legitimate User Connectivity Test

### Device

PC-Client1

### Commands

```bash
ping 192.168.2.10
ping 192.168.2.11
ping 192.168.2.12
```

### Expected Result

All legitimate pings succeed.

---

## 3. DoS-Style ICMP Blocking Test

### Device

PC-Attack

### Commands

```bash
ping 192.168.2.10
ping 192.168.2.11
ping 192.168.2.12
```

### Expected Result

```bash
Reply from 192.168.1.1: Destination host unreachable.
Packets: Sent = 4, Received = 0, Lost = 4 (100% loss)
```

---

## 4. ACL Match Counter Verification

### Device

Router-ACL

### Commands

```bash
enable
show access-lists
```

### Expected Result

```bash
10 deny icmp 192.168.1.0 0.0.0.255 192.168.2.0 0.0.0.255 (12 match(es))
```

---

## 5. Port Scanning Test

### Device

PC-Attack

### Commands

```bash
telnet 192.168.2.10 22
telnet 192.168.2.10 23
telnet 192.168.2.10 3389
```

### Expected Result

```bash
Trying 192.168.2.10 ...
% Connection timed out; remote host not responding
```

---

## 6. Port Security Baseline Check

### Device

SW-Core

### Commands

```bash
enable
show port-security
show port-security interface fa0/2
show interfaces status
```

### Expected Result

```bash
Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Shutdown
Maximum MAC Addresses      : 1
Sticky MAC Addresses       : 1
Security Violation Count   : 0
```

---

## 7. MAC Flooding / Port Security Violation Test

### Expected Result

```bash
Port Status                : Secure-shutdown
Security Violation Count   : 1

Fa0/2                      err-disabled
```

---

## 8. Syslog Logging Test

### Devices

Router-ACL and Syslog Server

### Commands

```bash
enable
configure terminal
interface g0/0/0
shutdown
no shutdown
end
```

### Expected Result

Syslog displays:

* LINK-5-CHANGED
* LINEPROTO-5-UPDOWN
* SYS-5-CONFIG_I

---

## 9. DHCP Snooping Protection Test

### Device

SW-Core

### Commands

```bash
enable
show ip dhcp snooping
show ip dhcp snooping binding
```

### Expected Result

* DHCP Snooping enabled
* Trusted interfaces configured
* Rogue DHCP behavior blocked

---

## 10. OSPF Routing Verification

### Device

Router0

### Commands

```bash
show ip route
show ip ospf neighbor
```

### Expected Result

* OSPF neighbors appear in FULL state
* Remote routes are learned correctly

---

## 11. SSH Administrative Access Verification

### Commands

```bash
ssh -l admin 192.168.2.1
```

### Expected Result

* Authorized SSH access succeeds
* Unauthorized access is blocked

---

## 12. Fake DHCP Server Simulation

### Device

Fake-DHCP-Server

### Expected Result

* Rogue DHCP activity is controlled
* DHCP Snooping prevents unauthorized DHCP influence

---

# Final Validation

## Final Confirmed Results

* ACL policies successfully block hostile ICMP traffic
* TCP ports 22, 23, and 3389 are protected
* DHCP Snooping operates correctly
* OSPF routing operates successfully
* Syslog receives supported events
* Port Security detects MAC violations
* Legitimate client traffic remains functional
* The topology is professionally segmented and organized

---

# Screenshots Required

Add screenshots for:

* Full topology map
* ACL blocking evidence
* Port scanning timeout
* Port Security violation
* Syslog logs
* DHCP Snooping verification

---

# Documentation Includes

* Attack-response logs
* Router ACL configurations
* Port Security configurations
* DHCP Snooping configurations
* Syslog screenshots
* Topology screenshots
* Visualization evidence

---

# Demo Video

Project Demo Video:
[https://drive.google.com/file/d/1jn9wrSEn-xO-9bFYxT41wxiAyFx7kZFQ/view?usp=sharing](https://drive.google.com/file/d/1jn9wrSEn-xO-9bFYxT41wxiAyFx7kZFQ/view?usp=sharing)

---

# Final Notes

THREAT_FINAL demonstrates a complete layered cybersecurity defense model using attack simulation, traffic filtering, switch protection, secure routing, centralized logging, and visualization techniques inside Cisco Packet Tracer.

```
```
