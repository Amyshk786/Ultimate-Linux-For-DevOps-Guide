# Day 4 – Linux Networking Commands

## Introduction

Linux networking commands help administrators and DevOps engineers inspect network interfaces, troubleshoot connectivity, diagnose DNS issues, check open ports, trace network paths, and monitor network traffic.

These commands are useful when working with:
- Linux servers and AWS EC2 instances
- Docker containers and Kubernetes
- DNS and IP address troubleshooting
- Firewall and port connectivity
- Network performance and packet loss
- Application and API connectivity

---

## 1. `ping` – Test Network Connectivity

The `ping` command checks whether a destination is reachable by sending ICMP Echo Request packets and waiting for Echo Reply packets.

It also displays round-trip time (latency) and packet loss.

**Command:**

```bash
ping google.com
```

Send only 4 packets:

```bash
ping -c 4 google.com
```

**What to observe:**
- `time`: Round-trip time in milliseconds.
- `ttl`: Time To Live value in the response.
- `packet loss`: Percentage of packets that did not receive a reply.

**DevOps use case:** Check basic connectivity when an application or server cannot reach another host.

Note: A failed ping does not always mean the destination is down. Firewalls may block ICMP traffic.

---

## 2. `netstat` – Display Network Connections

`netstat` displays active network connections, listening ports, routing tables, and network interface statistics.

Install on Ubuntu/Debian:

```bash
sudo apt update
sudo apt install net-tools
```

Display connections:

```bash
netstat
```

Useful options:

```bash
netstat -tuln
netstat -tulnp
netstat -an
netstat -r
```

| Option | Meaning |
|---|---|
| `-t` | TCP connections |
| `-u` | UDP connections |
| `-l` | Listening sockets |
| `-n` | Display numeric IPs and ports |
| `-p` | Display process information where permitted |
| `-a` | Display all sockets |
| `-r` | Display routing table |

Example:

```bash
sudo netstat -tulnp
```

This helps identify which processes are listening on network ports.

**Modern alternative:** `ss` is generally preferred on modern Linux systems.

---

## 3. `ifconfig` – Network Interface Configuration

`ifconfig` displays or configures network interface information, including IP addresses, netmasks, and interface status.

Install:

```bash
sudo apt install net-tools
```

Display interfaces:

```bash
ifconfig
```

Display a specific interface:

```bash
ifconfig ens5
```

**Important:** `ifconfig` is an older utility. Modern Linux systems generally use the `ip` command.

---

## 4. `traceroute` – Trace the Network Path

`traceroute` identifies the network hops packets pass through to reach a destination.

Each hop represents a router or network device along the path.

Install:

```bash
sudo apt install traceroute
```

Run:

```bash
traceroute youtube.com
```

Example output:

```text
traceroute to youtube.com
 1   240.2.196.12   1.063ms  0.981ms  0.988ms
 2   242.6.253.5    0.775ms  0.990ms  1.112ms
```

**How it works:**

Traceroute sends probes with increasing TTL (Time To Live) values. When a packet's TTL expires, an intermediate router may return an ICMP Time Exceeded response.

**DevOps use case:** Investigate routing problems, unexpected network paths, and latency between servers.

Some routers do not respond to traceroute probes. A missing response does not necessarily mean traffic cannot pass through that hop.

---

## 5. `tracepath` – Trace Network Path and Discover MTU

`tracepath` is another network diagnostic tool. It traces the route to a destination and can discover the Path Maximum Transmission Unit (PMTU).

Install if required:

```bash
sudo apt install iputils-tracepath
```

Run:

```bash
tracepath trainwithshubham.com
```

Example output:

```text
1?: [LOCALHOST]                      pmtu 9001
1:  ip-172-31-0-1.ap-south-1.compute.internal  0.075ms pmtu 1500
2:  no reply
3:  no reply
4:  52.95.67.55                      0.728ms
```

**Key terms:**
- `PMTU`: Maximum packet size that can travel along a network path without fragmentation, subject to the network's behavior.
- `no reply`: A hop did not return a response to the probe.
- `hop`: An intermediate network device.

### Traceroute vs Tracepath

| Feature | Traceroute | Tracepath |
|---|---|---|
| Purpose | Trace network path | Trace path and discover PMTU |
| Privileges | Depends on probe method and configuration | Usually does not require root |
| Options | Generally more configurable | Simpler interface |
| MTU discovery | Available with suitable options | Built-in PMTU discovery |

---

## 6. `mtr` – My Traceroute

`mtr` combines the functionality of `ping` and `traceroute`.

It continuously probes network hops and displays latency and packet-loss statistics.

Install:

```bash
sudo apt install mtr
```

Run:

```bash
mtr trainwithshubham.com
```

Useful options:

```bash
mtr -rw trainwithshubham.com
mtr -c 10 trainwithshubham.com
```

**Important output fields:**

| Field | Meaning |
|---|---|
| `Loss%` | Percentage of probes without a response |
| `Snt` | Number of probes sent |
| `Last` | Last recorded round-trip time |
| `Avg` | Average round-trip time |
| `Best` | Lowest recorded round-trip time |
| `Wrst` | Highest recorded round-trip time |
| `StDev` | Standard deviation of latency |

**DevOps use case:** Diagnose intermittent packet loss or high latency between an application server and an external service.

A router may deprioritize diagnostic responses, so packet loss at an intermediate hop does not automatically mean it is dropping forwarded traffic. Check whether the loss continues to later hops.

---

## 7. `nslookup` – DNS Lookup

`nslookup` queries DNS servers to retrieve information about domain names and IP addresses.

Command:

```bash
nslookup trainwithshubham.com
```

Example output:

```text
Server:         127.0.0.53
Address:        127.0.0.53#53

Non-authoritative answer:
Name:   trainwithshubham.com
Address: 15.197.225.128
Name:   trainwithshubham.com
Address: 3.33.251.168
```

**Understanding the output:**
- `Server`: DNS resolver used for the query.
- `127.0.0.53`: Local DNS stub resolver commonly used by systemd-resolved on Ubuntu.
- `Non-authoritative answer`: The response came from a recursive resolver or its cache, rather than directly from the domain's authoritative nameserver.
- `Address`: IP address returned for the domain.

Query a specific DNS server:

```bash
nslookup google.com 8.8.8.8
```

**DevOps use case:** Troubleshoot DNS resolution problems when a server cannot resolve a domain name.

---

## 8. `telnet` – Test TCP Port Connectivity

Telnet is a text-based network protocol and client. It can also be used to test whether a TCP connection can be established to a particular host and port.

Install:

```bash
sudo apt install telnet
```

Test port 80:

```bash
telnet trainwithshubham.com 80
```

Example:

```text
Trying 3.33.251.168...
Connected to trainwithshubham.com.
Escape character is '^]'.
```

**Meaning:** The TCP connection to the destination port was established.

Test other ports:

```bash
telnet example.com 443
telnet 192.168.1.10 22
```

**Important:** Telnet does not provide TLS encryption. Use it only for appropriate connectivity tests, not for secure remote administration.

Modern alternatives include:

```bash
nc -vz example.com 443
curl -Iv https://example.com
```

---

## 9. `hostname` – Display System Hostname

The `hostname` command displays or manages the system hostname.

Display hostname:

```bash
hostname
```

Display fully qualified domain name, if configured:

```bash
hostname -f
```

Display hostname information:

```bash
hostnamectl
```

Example:

```text
ip-172-31-1-139
```

**DevOps use case:** Identify servers in cloud environments, scripts, and monitoring systems.

---

## 10. `ip` – Modern Network Configuration Tool

The `ip` command is the modern replacement for many older networking utilities, including `ifconfig` and `route`.

Display IP addresses:

```bash
ip addr
```

Short form:

```bash
ip a
```

Display network interfaces:

```bash
ip link show
```

Display routing table:

```bash
ip route
```

Display neighbor/ARP table:

```bash
ip neigh
```

### Understanding `ip addr` output

Example:

```text
1: lo: <LOOPBACK,UP,LOWER_UP>
    inet 127.0.0.1/8

2: ens5: <BROADCAST,MULTICAST,UP,LOWER_UP>
    inet 172.31.1.139/20
    brd 172.31.15.255

3: br-55f787d4abbd:
    inet 172.18.0.1/16

4: docker0:
    inet 172.17.0.1/16
```

**Understanding the interfaces:**

| Interface / Address | Explanation |
|---|---|
| `lo` | Loopback interface |
| `127.0.0.1` | Localhost IPv4 address |
| `ens5` | Network interface commonly used by an AWS EC2 Linux instance |
| `172.31.1.139` | Private IPv4 address assigned to the EC2 network interface |
| `172.31.15.255` | Broadcast address for the displayed `/20` subnet |
| `br-...` | Docker-created bridge network interface |
| `172.18.0.1` | IP address of the displayed Docker bridge |
| `docker0` | Default Docker bridge interface |
| `172.17.0.1` | Default Docker bridge gateway address |

**Important networking concepts:**

- `inet` indicates an IPv4 address.
- `inet6` indicates an IPv6 address.
- `brd` indicates the broadcast address.
- `/20` and `/16` represent CIDR prefix lengths.
- `UP` indicates the interface is administratively enabled.
- `LOWER_UP` indicates the underlying link is operational.

An EC2 instance's private IP is not necessarily its public IP. AWS networking can associate a public IPv4 address or Elastic IP separately.

---

## 11. `iwconfig` – Wireless Interface Information

`iwconfig` displays or configures wireless network interface parameters.

Install:

```bash
sudo apt install wireless-tools
```

Run:

```bash
iwconfig
```

Example:

```text
lo        no wireless extensions.
ens5      no wireless extensions.
docker0   no wireless extensions.
```

**Why does it show `no wireless extensions`?**

The displayed interfaces are not wireless network interfaces. For example, an AWS EC2 Ethernet interface generally does not provide Wi-Fi functionality.

---

## 12. `ss` – Socket Statistics

`ss` displays socket information, including TCP, UDP, and listening connections.

It is a modern and generally preferred alternative to `netstat`.

Useful commands:

```bash
ss -tuln
ss -tulnp
ss -s
ss -ant
```

| Option | Meaning |
|---|---|
| `-t` | TCP sockets |
| `-u` | UDP sockets |
| `-l` | Listening sockets |
| `-n` | Numeric addresses and ports |
| `-p` | Process information |
| `-a` | All sockets |
| `-s` | Socket summary |

Check whether an application is listening on port 8080:

```bash
sudo ss -tulnp | grep :8080
```

**DevOps use case:** Find which service is listening on a port when troubleshooting application connectivity.

---

## 13. `arp` – Address Resolution Protocol

ARP stands for Address Resolution Protocol.

It helps resolve an IPv4 address to a MAC address on a local network segment.

Display the ARP cache:

```bash
arp
```

Modern alternative:

```bash
ip neigh
```

Example:

```text
Address                  HWtype  HWaddress
ip-172-31-0-2             ether   0a:e3:cb:35:82:ee
```

**Important:** ARP operates between the network and data-link layers in the practical TCP/IP networking model. It is used for IPv4 address resolution on a local link. IPv6 uses Neighbor Discovery Protocol (NDP), not ARP.

---

## 14. `dig` – Detailed DNS Query

`dig` is a DNS lookup utility that provides detailed DNS response information.

Run:

```bash
dig trainwithshubham.com
```

Query specific record types:

```bash
dig google.com A
dig google.com AAAA
dig google.com MX
dig google.com NS
dig google.com TXT
```

Query a particular DNS resolver:

```bash
dig @8.8.8.8 google.com
```

Useful options:

```bash
dig +short google.com
dig +trace google.com
```

### Understanding `dig` output

Example:

```text
;; ->>HEADER<<- opcode: QUERY, status: NOERROR
;; QUESTION SECTION:
;trainwithshubham.com. IN A

;; ANSWER SECTION:
trainwithshubham.com. 300 IN A 3.33.251.168
trainwithshubham.com. 300 IN A 15.197.225.128
```

| Field | Meaning |
|---|---|
| `NOERROR` | DNS query completed successfully |
| `A` | IPv4 address record |
| `300` | TTL in seconds |
| `IN` | Internet DNS class |
| `ANSWER SECTION` | DNS records returned |
| `SERVER` | DNS server that answered the query |
| `Query time` | Time taken to receive the response |

**DevOps use case:** Troubleshoot Route 53 records, DNS propagation, domain resolution, and application connectivity.

---

## 15. `nc` – Netcat

Netcat is a versatile networking utility used to read from and write to network connections.

It is often described as the Swiss Army knife of networking.

Install:

```bash
sudo apt install netcat-openbsd
```

Check whether a TCP port is reachable:

```bash
nc -vz example.com 443
```

Check an internal server:

```bash
nc -vz 192.168.1.10 8080
```

Listen on a port for a basic test:

```bash
nc -l 8080
```

**DevOps use case:** Test connectivity between application servers, databases, and services.

Only use listening or connection tests on systems and ports you are authorized to access.

---

## 16. `whois` – Domain Registration Information

`whois` queries public domain registration databases.

Install:

```bash
sudo apt install whois
```

Run:

```bash
whois trainwithshubham.com
```

Information may include:
- Registrar
- Domain creation date
- Domain expiry date
- Nameservers
- Domain status
- Registration details, where publicly available

**DevOps use case:** Investigate domain registration and nameserver information.

Note: Privacy protection and registry policies may hide some registration details.

---

## 17. `ifplugstatus` – Ethernet Link Status

`ifplugstatus` checks the link status of network interfaces.

Install:

```bash
sudo apt install ifplugd
```

Run:

```bash
ifplugstatus
```

Example:

```text
lo: link beat detected
ens5: link beat detected
br-55f787d4abbd: unplugged
docker0: unplugged
```

This utility is mainly useful for physical Ethernet link detection. Virtual interfaces may report different states.

Modern alternative for interface status:

```bash
ip link show
```

---

## 18. `route` – Display Routing Table

The `route` command displays or manipulates the IP routing table.

Display routes:

```bash
route -n
```

Install if required:

```bash
sudo apt install net-tools
```

Modern alternative:

```bash
ip route
```

Example:

```text
default via 172.31.0.1 dev ens5
172.31.0.0/20 dev ens5 proto kernel scope link
```

**Understanding the output:**

- `default`: Default route used when no more specific route matches.
- `via`: Next-hop gateway.
- `dev`: Network interface used.
- `172.31.0.0/20`: Connected network route.

**DevOps use case:** Troubleshoot incorrect gateways, missing routes, and network reachability.

---

## 19. `nmap` – Network Exploration and Port Scanning

Nmap stands for Network Mapper.

It is used for network discovery, host detection, port scanning, and security auditing.

Install:

```bash
sudo apt install nmap
```

Scan a host:

```bash
nmap youtube.com
```

Verbose scan:

```bash
nmap -v youtube.com
```

Scan a specific port:

```bash
nmap -p 443 example.com
```

Scan a range of ports:

```bash
nmap -p 1-1000 192.168.1.10
```

Check common ports:

```bash
nmap -F example.com
```

Example output:

```text
PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  https
```

**Understanding port states:**

- `open`: A service is accepting connections.
- `closed`: The host responds, but no service is listening on the port.
- `filtered`: Nmap cannot determine whether the port is open because filtering prevents a clear response.

**DevOps use case:** Validate exposed services and investigate network security configurations.

**Security warning:** Only scan systems and networks you own or have explicit permission to test. Follow your organization's security policies.

---

## 20. `wget` – Download Files

`wget` is a command-line utility used to download files from web servers.

Download a file:

```bash
wget https://example.com/file.zip
```

Save with a custom filename:

```bash
wget -O application.zip https://example.com/file.zip
```

Continue an interrupted download:

```bash
wget -c https://example.com/file.zip
```

Download a website recursively:

```bash
wget --mirror https://example.com
```

**DevOps use case:** Download packages, scripts, configuration files, and application artifacts.

Be careful when downloading and executing scripts from the internet. Verify the source first.

---

## 21. `watch` – Execute Commands Repeatedly

`watch` runs a command periodically and displays its output.

By default, it refreshes every two seconds.

Examples:

```bash
watch top
watch free -h
watch df -h
watch ss -tuln
```

Monitor a command every five seconds:

```bash
watch -n 5 free -h
```

Highlight differences between updates:

```bash
watch -d free -h
```

Exit using:

```text
Ctrl + C
```

**DevOps use case:** Monitor disk usage, memory, processes, and listening ports during troubleshooting.

---

## 22. `iptables` – Linux Firewall Management

`iptables` is a command-line utility used to manage packet-filtering and NAT rules in Linux.

It can control:
- Incoming traffic
- Outgoing traffic
- Forwarded traffic
- Port forwarding
- Network Address Translation (NAT)

Display existing rules:

```bash
sudo iptables -L -n -v
```

Display NAT rules:

```bash
sudo iptables -t nat -L -n -v
```

List rules with line numbers:

```bash
sudo iptables -L --line-numbers
```

**Important concepts:**

| Chain | Purpose |
|---|---|
| `INPUT` | Traffic destined for the local machine |
| `OUTPUT` | Traffic generated by the local machine |
| `FORWARD` | Traffic routed through the machine |

**DevOps use case:** Understand host-level firewall rules and troubleshoot blocked connections.

Modern Linux distributions may use nftables underneath, and tools such as UFW may manage firewall rules through a higher-level interface. Always inspect the existing firewall configuration before changing rules.

---

## 23. `curl` vs `wget` – HTTP Requests and Downloads

Both `curl` and `wget` can communicate with web servers, but they are commonly used for different tasks.

### wget

Use `wget` when you mainly need to download files, resume downloads, or mirror websites.

```bash
wget https://example.com/file.zip
```

### curl

Use `curl` when you need to interact with APIs, send HTTP requests, use custom headers, or inspect HTTP responses.

Check website headers:

```bash
curl -I https://example.com
```

Make a GET request:

```bash
curl https://example.com
```

Make a POST request:

```bash
curl -X POST https://example.com/api
```

Send a custom header:

```bash
curl -H "Content-Type: application/json" https://example.com/api
```

### Example: Call an API and format JSON using jq

Install jq:

```bash
sudo apt install jq
```

Call an API:

```bash
curl -X GET https://dummy.restapiexample.com/api/v1/employees | jq
```

**Understanding the command:**

- `curl`: Sends the HTTP request.
- `-X GET`: Specifies the HTTP method.
- API URL: Endpoint being called.
- `|`: Sends the output to another command.
- `jq`: Formats and processes JSON data.

Useful curl options:

```bash
curl -v https://example.com
curl -s https://example.com
curl -o output.txt https://example.com
curl -L https://example.com
curl -w "%{http_code}\n" -o /dev/null -s https://example.com
```

| Option | Meaning |
|---|---|
| `-v` | Verbose request and connection details |
| `-s` | Silent mode |
| `-o` | Save response to a file |
| `-L` | Follow redirects |
| `-I` | Fetch response headers |
| `-H` | Add a custom header |
| `-X` | Specify HTTP method |

---

# Quick Revision – Networking Commands

| Command | Main Purpose |
|---|---|
| `ping` | Check network reachability and latency |
| `netstat` | Display network connections and listening ports |
| `ifconfig` | Display/configure network interfaces |
| `traceroute` | Trace network path |
| `tracepath` | Trace path and discover PMTU |
| `mtr` | Continuous ping and route diagnostics |
| `nslookup` | Query DNS |
| `telnet` | Test TCP connectivity |
| `hostname` | Display system hostname |
| `ip` | Manage IP addresses, interfaces, and routes |
| `iwconfig` | Display wireless interface information |
| `ss` | Display socket statistics |
| `arp` | Display IPv4-to-MAC neighbor cache |
| `dig` | Perform detailed DNS queries |
| `nc` | Test or establish network connections |
| `whois` | Query domain registration information |
| `ifplugstatus` | Check Ethernet link status |
| `route` | Display routing table |
| `nmap` | Discover hosts and scan ports |
| `wget` | Download files |
| `watch` | Run commands periodically |
| `iptables` | Manage firewall and NAT rules |
| `curl` | Make HTTP requests and interact with APIs |

---

# Practical Troubleshooting Scenarios

## Scenario 1: Website is not reachable

```bash
ping google.com
curl -I https://google.com
```

Check whether basic connectivity and HTTPS access work.

## Scenario 2: DNS is not resolving

```bash
nslookup example.com
dig example.com
```

Check whether the domain resolves and which DNS resolver responds.

## Scenario 3: Application is not accessible on port 8080

```bash
sudo ss -tulnp | grep :8080
nc -vz 192.168.1.10 8080
```

Check whether the application is listening and whether the remote TCP connection succeeds.

## Scenario 4: Network latency or packet loss

```bash
ping -c 10 example.com
mtr example.com
traceroute example.com
```

Investigate latency and packet loss along the network path.

## Scenario 5: Server cannot reach another network

```bash
ip addr
ip route
ip neigh
```

Inspect the server's IP configuration, routing table, and neighbor information.

## Scenario 6: Check whether HTTPS is working

```bash
curl -Iv https://example.com
```

Inspect the connection, TLS handshake, certificate information, and HTTP response headers.

---

# Interview Questions

1. What is the difference between `ping` and `traceroute`?
2. What is the difference between `netstat` and `ss`?
3. What is the difference between `ifconfig` and `ip addr`?
4. What is the difference between `nslookup` and `dig`?
5. What is the difference between `curl` and `wget`?
6. What is the difference between `traceroute` and `tracepath`?
7. What is the purpose of the `mtr` command?
8. How do you check whether a port is listening in Linux?
9. How do you check whether a remote TCP port is reachable?
10. What is the difference between an IP address and a MAC address?
11. What is ARP and why is it required?
12. How do you check the default gateway in Linux?
13. What is the purpose of `iptables`?
14. How would you troubleshoot a DNS resolution issue?
15. How would you troubleshoot an application that is not reachable from another server?

---

# Hands-on Practice

Run these commands on a Linux machine or an AWS EC2 instance that you are authorized to use.

```bash
# 1. Check connectivity
ping -c 4 google.com

# 2. Display IP addresses
ip addr

# 3. Display routing table
ip route

# 4. Display listening TCP and UDP ports
sudo ss -tulnp

# 5. Perform DNS lookup
nslookup google.com

# 6. Query DNS records
dig google.com

# 7. Trace network path
traceroute google.com

# 8. Check TCP port connectivity
nc -vz google.com 443

# 9. Check HTTP response
curl -I https://google.com

# 10. Display network neighbors
ip neigh

# 11. Monitor memory periodically
watch -n 2 free -h

# 12. Check hostname
hostname
```

## Learning Outcome

After practicing these commands, you should be able to:

- Check connectivity between Linux servers.
- Understand IP addresses and network interfaces.
- Inspect listening ports and active connections.
- Troubleshoot DNS resolution.
- Trace network paths and investigate latency.
- Test application and API connectivity.
- Understand basic Linux firewall and routing commands.

**Next topic:** Linux process management, services, and system monitoring.
