# ThreatMap - Network Attack Simulation & Visualization

ThreatMap is a Cisco Packet Tracer project that demonstrates how common network attacks affect a segmented network and how basic defenses respond in real time.

The project simulates:
- DoS-style service disruption using blocked ICMP traffic
- Port Scanning against protected management ports
- MAC Flooding detection and shutdown using Port Security

The project also shows:
- Router ACL enforcement
- Switch Port Security reaction
- Syslog event collection
- Visual network topology and evidence screenshots

## Repository Contents

### `Project 25 ThreatMap.pkt`
This is the main Cisco Packet Tracer simulation file.

Use this file if you want to:
- Open the full network topology
- Run the attacks manually
- Verify ACL behavior on the router
- Verify Port Security behavior on the switch
- Check Syslog events inside Packet Tracer

### `ThreatMap.pdf`
This is the main written report.

Use this file if you want to:
- Read the project summary
- Understand the topology and security design
- Review the attack-response explanation
- See the documented conclusions

### `screenshots.docx`
This file contains the project evidence and visual documentation.

Use this file if you want to:
- Review screenshots of the topology
- See ACL configuration and verification
- See Port Security before and after violation
- See attack results and Syslog proof

### `ThreatMap Test Checklist - Detailed.docx`
This file is the presentation and viva guide.

Use this file if you want to:
- Explain the project step by step
- Show what is tested in each stage
- Compare before and after results
- Use ready-made English wording during the demo

## Recommended Order To Open The Files

1. Open `ThreatMap.pdf` to understand the project quickly.
2. Open `Project 25 ThreatMap.pkt` if you want to run the simulation.
3. Open `screenshots.docx` to review visual proof and evidence.
4. Open `ThreatMap Test Checklist - Detailed.docx` before presenting the project.

## Main Security Controls Used

- Extended ACL named `ANTI-DOS` on `Router-ACL`
- `ip access-group ANTI-DOS in` on `GigabitEthernet0/0/0`
- Port Security on `SW-Core Fa0/2`
- Syslog server at `192.168.2.200`

## Verified Attack Scenarios

### 1. DoS-Style ICMP Blocking
`PC-Attack` sends repeated ICMP traffic toward the protected servers.

Expected result:
- The router blocks the traffic
- The attacker receives `Destination host unreachable`
- ACL match counters increase

### 2. Port Scanning
`PC-Attack` probes protected host ports `22`, `23`, and `3389`.

Expected result:
- Connection attempts time out
- Sensitive management ports remain inaccessible from the attacker zone

### 3. MAC Flooding / Port Security Violation
The protected switch port is tested against unauthorized MAC or device behavior.

Expected result:
- `Fa0/2` changes from `Secure-up` to `Secure-shutdown`
- The interface becomes `err-disabled`
- The switch records a Port Security violation

## Logging Evidence

The Syslog server is used to capture supported Packet Tracer events such as:
- `%LINK-5-CHANGED`
- `%LINEPROTO-5-UPDOWN`
- `%SYS-5-CONFIG_I`

## Important Note

Cisco Packet Tracer does not fully support all real-world ACL logging features.  
Because of that, this project uses:
- Syslog-supported events
- ACL match counters
- Port Security status outputs

These are the main proof artifacts for the defensive response.

## If You Want To Re-Demo The Project

Open `Project 25 ThreatMap.pkt` and test:
- `show access-lists` on `Router-ACL`
- `show port-security interface fa0/2` on `SW-Core`
- `ping` tests from `PC-Client1`
- `ping` and `telnet` tests from `PC-Attack`
- Syslog view on the `Syslog Server`

## Suggested GitHub Upload Structure

Keep the repository simple:

```text
README.md
Project 25 ThreatMap.pkt
ThreatMap.pdf
screenshots.docx
ThreatMap Test Checklist - Detailed.docx
```

If you want clearer filenames later, you can optionally rename them to:
- `01-ThreatMap-Simulation.pkt`
- `02-ThreatMap-Report.pdf`
- `03-ThreatMap-Screenshots.docx`
- `04-ThreatMap-Test-Checklist.docx`
