---

<div align="center">

# MINI SOC USING WAZUH

</div>

A small security operations lab: a Windows 11 endpoint monitored with Sysmon, an Ubuntu endpoint monitored with Suricata, and a Kali attacker, with Wazuh as the central SIEM. All four VMs run on a VMware NAT network.

---

### Environment

| VM            | Role                            | OS             | Address          | Assignment |
|---------------|---------------------------------|----------------|------------------|------------|
| WazuhManager  | SIEM (Wazuh Manager, dashboard) | Ubuntu Server  | 192.168.121.10   | Static     |
| Windows11     | Endpoint (Sysmon)               | Windows 11     | 192.168.121.11   | Static     |
| UbuntuDesktop | Endpoint (Suricata)             | Ubuntu Desktop | 192.168.121.24   | Static     |
| KaliLinux     | Attacker                        | Kali Linux     | 192.168.121.25   | Static     |

Network: VMware NAT (VMnet8), `192.168.121.0/24`, gateway `192.168.121.2`.

<div align="center">

<img src="mini-soc-topology.png" alt="Lab topology" width="700">

</div>

---

### What was built

- Four VMs on a VMware NAT network with static IPs and Internet access.
- Sysmon on Windows11 using the SwiftOnSecurity configuration, running as a service.
- Sysmon process creation (Event ID 1) validated with `whoami`, `net user`, and `notepad`.

---

## Lab parts

### Part 1: Environment setup
[`01-Host-Setup.docx`](Jeffar%20Documentation/01-Host-Setup.docx), [`02-Network-and-IP-Configuration.docx`](Jeffar%20Documentation/02-Network-and-IP-Configuration.docx)

VMnet8 was set to `192.168.121.0/24` on the host. The four VMs were given static addresses on that network, and Windows11 was set to answer inbound ping. Connectivity was tested from Windows11 to every other VM and from each VM to the Internet.

**Evidence:** Pings from Windows11 to `192.168.121.10`, `192.168.121.24`, `192.168.121.25` and `8.8.8.8`, and pings to `8.8.8.8` from the other three VMs.

**Verified:** All pings succeed and every VM reaches the Internet.

### Part 2: Sysmon on Windows11
[`03-Sysmon.docx`](Jeffar%20Documentation/03-Sysmon.docx)

Sysmon was installed from Sysinternals with the SwiftOnSecurity configuration. From an elevated PowerShell session, `whoami`, `net user testuser /add` and `notepad.exe` were run and traced in the Sysmon Operational log.

**Evidence:** Event ID 1 (Process Create) for `whoami.exe`, `net.exe` with its child `net1.exe`, and `notepad.exe`, each with image, command line and user.

**Verified:** Events appear in Event Viewer under Sysmon, Operational.

---

### Documentation

Each student documents their own parts: [`Jeffar Documentation/`](Jeffar%20Documentation/), [`Matthew Documentation/`](Matthew%20Documentation/).
