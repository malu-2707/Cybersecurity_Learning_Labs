# Module 1: Cybersecurity & Networking Foundations

**Duration:** Day 1–Day 5
**Environment:** Kali Linux running in a virtual machine
**Purpose:** Build foundational knowledge of cybersecurity, Linux, networking, DNS, ports, and basic troubleshooting.

---

# Day 1 — Introduction to Cybersecurity and Linux

## 1. Learning objectives

* Understand the fundamentals of cybersecurity.
* Learn the CIA triad.
* Become familiar with Kali Linux.
* Identify the operating system, user, and working directory.
* Practise basic Linux commands.

## 2. What is cybersecurity?

Cybersecurity is the practice of protecting systems, networks, applications, and data against unauthorized access, attacks, damage, and theft.

### The CIA triad

**Confidentiality:** Information is accessible only to authorized people.

Example: Password protection and encryption.

**Integrity:** Information remains accurate and is not changed without authorization.

Example: File integrity verification.

**Availability:** Systems and information remain accessible when needed.

Example: Backups and system redundancy.

## 3. Introduction to Kali Linux

Kali Linux is a Debian-based Linux distribution used for penetration testing, security research, and digital forensics.

### My lab environment

* Operating system: Kali GNU/Linux Rolling
* Version: 2026.3
* Username: `malu`
* Home directory: `/home/malu`
* Network interface: `eth0`

## 4. Practical lab: Identify the operating system

**Command:**

```bash
cat /etc/os-release
```

**Observed output:**

```text
PRETTY_NAME="Kali GNU/Linux Rolling"
NAME="Kali GNU/Linux"
VERSION_ID="2026.3"
VERSION="2026.3"
VERSION_CODENAME=kali-rolling
ID=kali
ID_LIKE=debian
```

**Result:** Confirmed that the system is running Kali Linux Rolling.

## 5. Practical lab: Identify the current user and directory

**Command:**

```bash
pwd
```

**My answer/output:**

```text
/home/malu
```

**Meaning:** The current working directory is my home directory.

**Command:**

```bash
whoami
```

**My answer/output:**

```text
malu
```

**Meaning:** I am working under the regular user account `malu`.

## 6. Important Linux commands

| Command    | Purpose                               |
| ---------- | ------------------------------------- |
| `pwd`      | Show the current directory            |
| `whoami`   | Show the current username             |
| `ls`       | List files and directories            |
| `cd`       | Change directories                    |
| `cat`      | Display file contents                 |
| `id`       | Show user and group IDs               |
| `uname -a` | Display system and kernel information |

## 7. Day 1 summary

I learned the purpose of cybersecurity, the CIA triad, and the role of Kali Linux. I identified my operating system, username, and working directory using the terminal.

**Status:** Completed.

---

# Day 2 — IP Addressing and Network Configuration

## 1. Learning objectives

* Understand IP and MAC addresses.
* Identify a network interface.
* Find the default gateway.
* Understand local and remote network communication.

## 2. Important networking concepts

**IP address:** A logical address used to identify an interface on an IP network.

**MAC address:** A link-layer address associated with a network interface.

**Network interface:** The component through which a device connects to a network.

**Default gateway:** The router or next-hop device used to reach destinations outside the directly connected network.

**Loopback address:** An address used by a computer to communicate with itself. The IPv4 loopback address is `127.0.0.1`.

## 3. Practical lab: Inspect network interfaces

**Command:**

```bash
ip addr
```

**My observed results:**

| Item           | Value               |
| -------------- | ------------------- |
| Interface      | `eth0`              |
| IPv4 address   | `172.31.68.46`      |
| Network prefix | `/20`               |
| MAC address    | `00:0c:29:f1:93:8a` |
| Loopback IPv4  | `127.0.0.1`         |

The interface `eth0` was up and had an assigned IPv4 address.

## 4. Practical lab: Inspect routing

**Command:**

```bash
ip route
```

**My output:**

```text
default via 172.31.64.1 dev eth0 proto dhcp src 172.31.68.46 metric 100
172.31.64.0/20 dev eth0 proto kernel scope link src 172.31.68.46
```

**Interpretation:**

* Default gateway: `172.31.64.1`
* Network interface: `eth0`
* Kali IPv4 address: `172.31.68.46`
* Directly connected network: `172.31.64.0/20`

The default route indicates that Kali sends traffic for destinations without a more specific route through `172.31.64.1`.

## 5. Day 2 summary

I learned how to identify my network interface, IP address, MAC address, loopback address, and default gateway.

**Status:** Completed.

---

# Day 3 — Connectivity Testing and DNS

## 1. Learning objectives

* Test network connectivity.
* Understand the purpose of `ping`.
* Distinguish IP connectivity from domain-name resolution.
* Learn the basics of DNS.

## 2. Important concepts

**Ping:** Uses ICMP Echo Request and Echo Reply messages to test whether a destination responds.

**DNS:** The Domain Name System translates domain names into records such as IP addresses.

**IPv4:** Uses 32-bit addresses.

**IPv6:** Uses 128-bit addresses.

## 3. Practical lab: Test the default gateway

**Command:**

```bash
ping -c 4 172.31.64.1
```

**My result:**

* Packets transmitted: 4
* Packets received: 4
* Packet loss: 0%
* Average round-trip time: approximately 1.433 ms

**Conclusion:** The gateway responded successfully to the ping test.

## 4. Practical lab: Test external IP connectivity

**Command:**

```bash
ping -c 4 1.1.1.1
```

**My result:**

* Packets transmitted: 4
* Packets received: 4
* Packet loss: 0%
* Average round-trip time: approximately 56.309 ms

**Conclusion:** The external IP address responded successfully.

## 5. Practical lab: Test domain-name connectivity

**Command:**

```bash
ping -c 4 google.com
```

**My result:**

* Domain resolved to `142.251.221.110`
* Packets transmitted: 4
* Packets received: 4
* Packet loss: 0%
* Average round-trip time: approximately 36.147 ms

**Conclusion:** The domain resolved to an IP address and responded to the ping test.

Note: Successful ping results demonstrate that the destination responded to ICMP at that time. They do not guarantee that every service on that destination is available.

## 6. Practical lab: Inspect DNS resolution

**Command:**

```bash
nslookup google.com
```

**My observed results:**

* DNS server reported: `172.31.64.1`
* IPv4 address: `142.251.221.110`
* IPv6 address: `2404:6800:4007:836::200e`

The output also contained the message:

`Got recursion not available from 172.31.64.1`

Despite this warning, DNS records were returned successfully.

**Conclusion:** The lookup succeeded. The recursion warning is a separate DNS configuration or response detail; it does not mean the lookup itself failed.

## 7. Day 3 summary

I tested connectivity to my gateway and an external destination, then used DNS lookup tools to confirm that a domain name could resolve to IPv4 and IPv6 addresses.

**Status:** Completed.

---

# Day 4 — Ports, Processes, and Network Connections

## 1. Learning objectives

* Understand TCP and UDP ports.
* Identify listening services.
* Inspect established network connections.
* Associate sockets with processes.
* Recognize local-only services.

## 2. Important concepts

**Port:** A number used by transport protocols to identify a communication endpoint.

**Listening socket:** A socket waiting for incoming connections.

**Established connection:** A TCP connection whose handshake has completed.

**Loopback binding:** A service listening on a loopback address is generally accessible only from the same machine, unless another mechanism exposes it.

## 3. Practical lab: Inspect listening sockets

**Command:**

```bash
ss -tuln
```

Options:

* `-t`: TCP sockets
* `-u`: UDP sockets
* `-l`: Listening or unconnected sockets as applicable
* `-n`: Display numeric addresses and ports

## 4. Practical lab: Identify processes using listening ports

**Command:**

```bash
sudo ss -tulpn
```

**My observed results:**

| Process    |  PID |      Port | Binding               |
| ---------- | ---: | --------: | --------------------- |
| PostgreSQL | 1097 |  TCP 5432 | `127.0.0.1` and `::1` |
| Ollama     | 1014 | TCP 11434 | `127.0.0.1`           |

**Interpretation:**

* PostgreSQL was listening on the IPv4 and IPv6 loopback addresses.
* Ollama was listening on the IPv4 loopback address.
* These bindings indicate local-only listening rather than listening on every network interface.

The process names and socket information provide evidence of which services were listening at the time of the check.

## 5. Practical lab: Inspect TCP connections

**Command:**

```bash
ss -tn
```

This displayed active TCP connections, including connections to remote HTTPS endpoints on port `443`.

The output also included a connection in the `SYN-SENT` state to:

`172.25.227.102:1514`

A connection in `SYN-SENT` means a TCP connection attempt has started but the handshake has not completed.

## 6. Identify the process behind the connection

**Command:**

```bash
sudo ss -tnp
```

**My observation:** The pending connection was associated with:

`wazuh-agentd`, PID `1185`

Other established connections were associated with Firefox.

**Conclusion:** The pending connection was being attempted by the Wazuh agent process. The state alone does not establish why the connection failed.

## 7. Day 4 summary

I learned to inspect listening sockets, identify local services, and associate TCP connections with processes.

**Status:** Completed.

---

# Day 5 — Wazuh Troubleshooting and OSI Model

## 1. Learning objectives

* Understand the purpose of security monitoring.
* Investigate a failed service connection.
* Read service configuration and logs.
* Understand TCP ports and routing.
* Learn the OSI networking model.

## 2. What is Wazuh?

Wazuh is a security monitoring platform that provides capabilities such as log analysis, threat detection, configuration assessment, and endpoint monitoring.

A Wazuh agent communicates with a Wazuh manager to send information and receive relevant configuration or instructions.

## 3. Practical lab: Inspect Wazuh configuration

**Command:**

```bash
sudo grep -n -A 8 -B 2 '<client>' /var/ossec/etc/ossec.conf
```

**My observed configuration:**

```text
<client>
  <server>
    <address>172.25.227.102</address>
    <port>1514</port>
    <protocol>tcp</protocol>
  </server>
  <config-profile>kali, kali2026, kali2026.3</config-profile>
```

**Interpretation:**

* Configured manager: `172.25.227.102`
* Communication port: `1514`
* Transport protocol: TCP

## 4. Practical lab: Check the agent service

**Command:**

```bash
sudo systemctl status wazuh-agent --no-pager
```

**My result:**

* Service: `wazuh-agent`
* Status: `active (running)`
* Agent process: `wazuh-agentd`, PID `1185`

**Conclusion:** The agent service was running locally. However, a running service does not prove that it is successfully connected to its manager.

## 5. Practical lab: Inspect Wazuh logs

**Command:**

```bash
sudo tail -n 30 /var/ossec/logs/ossec.log
```

**Important observed messages:**

```text
Unable to connect to '[172.25.227.102]:1514/tcp'
Requesting a key from server: 172.25.227.102
Unable to connect to enrollment service at '[172.25.227.102]:1515'
Waiting for server reply (not started).
Unable to connect to any server.
```

The agent repeatedly attempted to connect but did not establish communication.

The logs also included a warning asking that the manager version be checked. This is a possible compatibility consideration, not proof that a version mismatch is the cause.

## 6. Practical lab: Check the route to the manager

**Command:**

```bash
ip route get 172.25.227.102
```

**My output:**

```text
172.25.227.102 via 172.31.64.1 dev eth0 src 172.31.68.46 uid 1000
cache
```

**Interpretation:**

* Destination: `172.25.227.102`
* Next hop: `172.31.64.1`
* Interface: `eth0`
* Source address: `172.31.68.46`

Kali had a route for the manager destination through its gateway. This did not prove that the manager itself was reachable.

## 7. Practical lab: Test the configured TCP ports

**Command:**

```bash
for p in 1514 1515; do
  timeout 3 bash -c "echo >/dev/tcp/172.25.227.102/$p" 2>/dev/null &&
  echo "Port $p reachable" ||
  echo "Port $p unreachable"
done
```

**My results:**

```text
Port 1514 unreachable
Port 1515 unreachable
```

**Conclusion:** Both TCP connection attempts failed from Kali during the test.

Possible causes include:

* The manager host or service is unavailable.
* A firewall or network rule is blocking traffic.
* The manager is not reachable from this VM's network.
* The service is not listening on the expected port.
* Configuration or enrollment requirements need attention.

The exact cause remains unconfirmed.

## 8. The OSI model

The Open Systems Interconnection (OSI) model describes network communication using seven conceptual layers.

| Layer | Name         | Examples or role                                      |
| ----: | ------------ | ----------------------------------------------------- |
|     7 | Application  | HTTP, DNS services                                    |
|     6 | Presentation | Data representation, encryption and encoding concepts |
|     5 | Session      | Session management concepts                           |
|     4 | Transport    | TCP, UDP, transport ports                             |
|     3 | Network      | IP addressing and routing                             |
|     2 | Data Link    | Ethernet frames and MAC addresses                     |
|     1 | Physical     | Transmission of bits over physical or radio media     |

### My quiz answers

**Question 1: Which OSI layer handles IP addresses and routing?**

My answer: **Networking**

Correct concept: **Layer 3 — Network**

**Question 2: Which OSI layer handles TCP and UDP ports?**

My answer: **Layer 4**

Result: **Correct**

### Memory aid

From Layer 7 down to Layer 1:

**All People Seem To Need Data Processing.**

## 9. Day 5 summary

I investigated a Wazuh agent that was running locally but failing to connect to its configured manager. I checked the configuration, service status, logs, routing decision, and TCP connectivity to the configured ports.

I also learned the OSI model and correctly identified Layer 4 as the Transport layer. My answer to the routing question was “Networking,” which pointed toward the right concept; the precise layer name is Layer 3 — Network.

**Status:** Practical troubleshooting completed; underlying Wazuh connectivity issue not yet resolved.

---

# Module 1 — Overall Review

## Skills practised

* Identifying a Linux distribution and user account.
* Navigating the Linux terminal.
* Inspecting IP addresses, MAC addresses, and routing.
* Testing connectivity with `ping`.
* Inspecting DNS with `nslookup`.
* Identifying listening sockets with `ss`.
* Inspecting processes and TCP connections.
* Checking a Linux service with `systemctl`.
* Reading configuration files and service logs.
* Testing authorized connectivity to a configured service.

## Important commands learned

```bash
cat /etc/os-release
pwd
whoami
ip addr
ip route
ping -c 4 172.31.64.1
ping -c 4 1.1.1.1
ping -c 4 google.com
nslookup google.com
ss -tuln
sudo ss -tulpn
ss -tn
sudo ss -tnp
sudo systemctl status wazuh-agent --no-pager
sudo tail -n 30 /var/ossec/logs/ossec.log
ip route get 172.25.227.102
```

## Key lessons

1. A running service is not necessarily reachable over the network.
2. A route to an IP address does not guarantee the destination is available.
3. DNS can resolve successfully even when a DNS warning appears.
4. A TCP connection in `SYN-SENT` has not completed its handshake.
5. Socket and process information help identify which applications communicate over the network.
6. Troubleshooting should be evidence-based; an error does not automatically mean a system is compromised.
7. Security testing must be limited to systems and networks I own or am explicitly authorized to assess.

## Final status

**Module 1 — Days 1–5: Foundations and practical exercises documented.**

The Wazuh connectivity issue is documented as an outstanding investigation rather than a confirmed security incident.

