# 🌐 Linux Networking Commands Reference

<div align="center">



**A comprehensive guide to essential Linux networking commands for system administrators, network engineers, and DevOps professionals.**



</div>

---

## 📋 Table of Contents

- [🌐 Linux Networking Commands Reference](#-linux-networking-commands-reference)
  - [📋 Table of Contents](#-table-of-contents)
  - [🎯 Overview](#-overview)
  - [🚀 Quick Start](#-quick-start)
  - [📡 Network Testing Commands](#-network-testing-commands)
    - [🏓 ping - Network Connectivity Testing](#-ping---network-connectivity-testing)
    - [🔍 traceroute - Network Path Tracing](#-traceroute---network-path-tracing)
    - [🛤️ tracepath - Path Discovery](#️-tracepath---path-discovery)
    - [📊 mtr - Network Diagnostic Tool](#-mtr---network-diagnostic-tool)
  - [⚙️ Network Configuration Commands](#️-network-configuration-commands)
    - [🔧 ifconfig - Network Interface Configuration](#-ifconfig---network-interface-configuration)
    - [🆔 ip - Modern Network Configuration](#-ip---modern-network-configuration)
    - [📶 iwconfig - Wireless Interface Configuration](#-iwconfig---wireless-interface-configuration)
    - [🏠 hostname - System Hostname](#-hostname---system-hostname)
  - [📊 Network Information Commands](#-network-information-commands)
    - [📈 netstat - Network Statistics](#-netstat---network-statistics)
    - [🔌 ss - Socket Statistics](#-ss---socket-statistics)
    - [🌍 whois - Domain Information](#-whois---domain-information)
    - [🗺️ arp - ARP Table Management](#️-arp---arp-table-management)
    - [🔌 ifplugstatus - Network Cable Status](#-ifplugstatus---network-cable-status)
  - [🌐 DNS Commands](#-dns-commands)
    - [🔍 nslookup - DNS Lookup](#-nslookup---dns-lookup)
    - [⚡ dig - Advanced DNS Lookup](#-dig---advanced-dns-lookup)
  - [📥 Data Transfer Commands](#-data-transfer-commands)
    - [🌊 curl - Data Transfer Tool](#-curl---data-transfer-tool)
    - [📦 wget - File Downloader](#-wget---file-downloader)
    - [🔗 telnet - Remote Connection](#-telnet---remote-connection)
  - [🛡️ Security & Monitoring Commands](#️-security--monitoring-commands)
    - [🧱 iptables - Firewall Configuration](#-iptables---firewall-configuration)
    - [👀 watch - Command Monitoring](#-watch---command-monitoring)
    - [🗺️ nmap - Network Scanner](#️-nmap---network-scanner)
    - [🛣️ route - Routing Table Management](#️-route---routing-table-management)
  - [💡 Quick Reference](#-quick-reference)
  - [🔧 Installation](#-installation)
  - [📚 Additional Resources](#-additional-resources)
  - [🤝 Contributing](#-contributing)
  - [📄 License](#-license)

---

## 🎯 Overview

This repository provides a comprehensive reference for essential Linux networking commands. Whether you're troubleshooting network issues, configuring interfaces, or monitoring network traffic, this guide covers the most important tools in the Linux networking toolkit.

### ✨ What You'll Learn

- **Network Testing**: Diagnose connectivity issues and measure network performance
- **Configuration**: Set up and manage network interfaces and routing
- **Monitoring**: Track network connections, traffic, and system resources
- **DNS Operations**: Resolve domains and troubleshoot DNS issues
- **Security**: Configure firewalls and scan networks
- **Data Transfer**: Download files and test network services

---

## 🚀 Quick Start

```bash
# Test network connectivity
ping google.com

# Check listening ports
ss -tuln

# View network interfaces
ip addr show

# Trace network path
traceroute google.com

# Check DNS resolution
dig google.com
```

---

## 📡 Network Testing Commands

### 🏓 ping - Network Connectivity Testing

**Purpose**: Send ICMP echo requests to test network connectivity and measure round-trip time.

```bash
# Basic usage
ping google.com
```
*Sends continuous ping packets to google.com until stopped with Ctrl+C.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-c count` | Send specific number of packets | `ping -c 4 google.com` | Sends exactly 4 packets then stops |
| `-i interval` | Set interval between packets | `ping -i 2 google.com` | Sends packets every 2 seconds |
| `-s size` | Set packet size in bytes | `ping -s 1000 google.com` | Sends 1000-byte packets |
| `-W timeout` | Set response timeout | `ping -W 5 192.168.1.1` | Waits max 5 seconds for response |
| `-f` | Flood ping (root only) | `sudo ping -f google.com` | Sends packets as fast as possible |
| `-q` | Quiet mode | `ping -q -c 4 google.com` | Shows only summary statistics |

### 🔍 traceroute - Network Path Tracing

**Purpose**: Trace the route packets take to reach a destination, showing each hop and timing.

```bash
# Basic usage
traceroute google.com
```
*Shows the complete path packets take to reach google.com.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-n` | Show IP addresses only | `traceroute -n google.com` | Faster execution, no DNS resolution |
| `-m max_ttl` | Set maximum hops | `traceroute -m 15 google.com` | Limits to 15 hops maximum |
| `-w timeout` | Set response timeout | `traceroute -w 3 google.com` | 3-second timeout per hop |
| `-I` | Use ICMP packets | `traceroute -I google.com` | Uses ICMP instead of UDP |
| `-T` | Use TCP packets | `traceroute -T google.com` | Uses TCP packets for tracing |
| `-p port` | Set destination port | `traceroute -p 80 google.com` | Traces to specific port |

### 🛤️ tracepath - Path Discovery

**Purpose**: Similar to traceroute but doesn't require root privileges, discovers MTU along path.

```bash
# Basic usage
tracepath google.com
```
*Traces path to google.com and shows MTU information.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-n` | Numeric IP addresses | `tracepath -n google.com` | Shows IPs instead of hostnames |
| `-b` | Print both hostname and IP | `tracepath -b google.com` | Shows both hostname and IP |
| `-m hops` | Set maximum hops | `tracepath -m 20 google.com` | Limits to 20 hops |
| `-4` | Force IPv4 | `tracepath -4 google.com` | Uses IPv4 only |
| `-6` | Force IPv6 | `tracepath -6 google.com` | Uses IPv6 only |

### 📊 mtr - Network Diagnostic Tool

**Purpose**: Combines ping and traceroute functionality for continuous network monitoring.

```bash
# Basic usage
mtr google.com
```
*Continuously traces route with real-time statistics.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-r, --report` | Report mode | `mtr -r -c 10 google.com` | Generates report after 10 packets |
| `-c count` | Number of packets | `mtr -c 5 google.com` | Sends 5 packets then stops |
| `-n, --no-dns` | No DNS resolution | `mtr -n google.com` | Shows IPs only, faster |
| `-i interval` | Set packet interval | `mtr -i 2 google.com` | 2-second intervals |
| `-s size` | Set packet size | `mtr -s 1000 google.com` | Uses 1000-byte packets |
| `--tcp` | Use TCP packets | `mtr --tcp google.com` | Uses TCP instead of ICMP |

---

## ⚙️ Network Configuration Commands

### 🔧 ifconfig - Network Interface Configuration

**Purpose**: Configure and display network interface parameters.

```bash
# Basic usage
ifconfig
```
*Displays configuration of all active network interfaces.*

#### 🚩 Essential Operations

| Operation | Description | Example | Usage |
|-----------|-------------|---------|-------|
| `ifconfig interface` | Show specific interface | `ifconfig eth0` | Shows eth0 configuration |
| `ifconfig -a` | Show all interfaces | `ifconfig -a` | Shows active and inactive interfaces |
| `ifconfig interface IP` | Assign IP address | `sudo ifconfig eth0 192.168.1.100` | Sets IP for eth0 |
| `ifconfig interface up/down` | Enable/disable interface | `sudo ifconfig eth0 down` | Disables eth0 |
| `ifconfig interface netmask` | Set netmask | `sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0` | Sets IP and netmask |
| `ifconfig interface mtu` | Set MTU size | `sudo ifconfig eth0 mtu 1500` | Sets MTU to 1500 bytes |

### 🆔 ip - Modern Network Configuration

**Purpose**: Comprehensive network configuration tool, modern replacement for ifconfig/route/arp.

```bash
# Basic usage
ip addr show
```
*Displays all network interfaces and their IP addresses.*

#### 🚩 Essential Subcommands

| Subcommand | Description | Example | Usage |
|------------|-------------|---------|-------|
| `ip addr` | Manage IP addresses | `ip addr show eth0` | Shows IP config for eth0 |
| `ip link` | Manage interfaces | `ip link show` | Shows all network interfaces |
| `ip route` | Manage routing | `ip route show` | Displays routing table |
| `ip neigh` | Manage ARP table | `ip neigh show` | Shows ARP entries |
| `-s, --stats` | Show statistics | `ip -s link show` | Shows interface statistics |
| `-4, -6` | IPv4/IPv6 only | `ip -4 addr show` | Shows IPv4 addresses only |

### 📶 iwconfig - Wireless Interface Configuration

**Purpose**: Configure wireless network interfaces.

```bash
# Basic usage
iwconfig
```
*Displays configuration of all wireless interfaces.*

#### 🚩 Essential Parameters

| Parameter | Description | Example | Usage |
|-----------|-------------|---------|-------|
| `essid` | Set network SSID | `sudo iwconfig wlan0 essid "MyWiFi"` | Connects to MyWiFi network |
| `key` | Set WEP key | `sudo iwconfig wlan0 key s:password` | Sets WEP encryption |
| `mode` | Set wireless mode | `sudo iwconfig wlan0 mode Managed` | Sets to managed mode |
| `channel` | Set wireless channel | `sudo iwconfig wlan0 channel 6` | Uses channel 6 |
| `freq` | Set frequency | `sudo iwconfig wlan0 freq 2.4G` | Sets 2.4GHz frequency |
| `power` | Power management | `sudo iwconfig wlan0 power off` | Disables power management |

### 🏠 hostname - System Hostname

**Purpose**: Display or set the system's network hostname.

```bash
# Basic usage
hostname
```
*Displays the current system hostname.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-i, --ip-address` | Show IP of hostname | `hostname -i` | Shows hostname's IP |
| `-I, --all-ip-addresses` | Show all IPs | `hostname -I` | Shows all system IPs |
| `-f, --fqdn` | Show FQDN | `hostname -f` | Shows fully qualified domain name |
| `-d, --domain` | Show domain name | `hostname -d` | Shows DNS domain |
| `-s, --short` | Show short hostname | `hostname -s` | Shows hostname up to first dot |

---

## 📊 Network Information Commands

### 📈 netstat - Network Statistics

**Purpose**: Display network connections, routing tables, and interface statistics.

```bash
# Basic usage
netstat -tuln
```
*Shows TCP and UDP listening ports with numerical addresses.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-a, --all` | Show all connections | `netstat -a` | Shows listening and non-listening |
| `-t, --tcp` | TCP connections only | `netstat -t` | Shows TCP connections |
| `-u, --udp` | UDP connections only | `netstat -u` | Shows UDP connections |
| `-l, --listening` | Listening ports only | `netstat -tl` | Shows TCP listening ports |
| `-n, --numeric` | Numerical addresses | `netstat -tn` | Shows IPs instead of hostnames |
| `-p, --programs` | Show process info | `netstat -tlnp` | Shows processes using ports |
| `-r, --route` | Show routing table | `netstat -r` | Displays kernel routing table |
| `-i, --interfaces` | Show interface stats | `netstat -i` | Shows interface statistics |

### 🔌 ss - Socket Statistics

**Purpose**: Modern replacement for netstat, faster and more detailed socket information.

```bash
# Basic usage
ss -tuln
```
*Shows TCP and UDP listening sockets with numerical addresses.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-t, --tcp` | TCP sockets | `ss -t` | Shows TCP connections |
| `-u, --udp` | UDP sockets | `ss -u` | Shows UDP connections |
| `-l, --listening` | Listening sockets | `ss -tl` | Shows TCP listening ports |
| `-n, --numeric` | Numerical addresses | `ss -tn` | Shows numerical addresses |
| `-p, --processes` | Show processes | `ss -tlnp` | Shows processes using ports |
| `-a, --all` | All sockets | `ss -a` | Shows all socket states |
| `-s, --summary` | Show statistics | `ss -s` | Shows socket usage summary |
| `-4, -6` | IPv4/IPv6 only | `ss -4` | Shows IPv4 sockets only |

### 🌍 whois - Domain Information

**Purpose**: Retrieve registration information for domains and IP addresses.

```bash
# Basic usage
whois google.com
```
*Shows registration details for google.com domain.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-h server` | Use specific whois server | `whois -h whois.arin.net 8.8.8.8` | Queries specific server |
| `-p port` | Use specific port | `whois -p 43 google.com` | Uses port 43 |
| `-H` | Hide legal disclaimers | `whois -H google.com` | Cleaner output |
| `-r` | Disable recursive lookups | `whois -r google.com` | No follow-up queries |
| `-R` | Enable recursive lookups | `whois -R google.com` | Forces recursive queries |

### 🗺️ arp - ARP Table Management

**Purpose**: Display and modify the ARP (Address Resolution Protocol) table.

```bash
# Basic usage
arp -a
```
*Shows all entries in the ARP table.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-a` | Show all entries | `arp -a` | Displays complete ARP table |
| `-n` | Numerical addresses | `arp -n` | Shows IP addresses only |
| `-d hostname` | Delete ARP entry | `sudo arp -d 192.168.1.1` | Removes ARP entry |
| `-s hostname hw_addr` | Add static entry | `sudo arp -s 192.168.1.1 aa:bb:cc:dd:ee:ff` | Adds static ARP entry |
| `-v` | Verbose output | `arp -av` | Shows detailed information |
| `-i interface` | Specific interface | `arp -a -i eth0` | Shows ARP entries for eth0 |

### 🔌 ifplugstatus - Network Cable Status

**Purpose**: Check physical connection status of network cables.

```bash
# Basic usage
ifplugstatus
```
*Shows cable connection status for all interfaces.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `ifplugstatus interface` | Check specific interface | `ifplugstatus eth0` | Shows cable status for eth0 |
| `-v, --verbose` | Verbose output | `ifplugstatus -v` | Shows detailed status |
| `-a, --all` | All interfaces | `ifplugstatus -a` | Shows status for all interfaces |
| `-w, --wait` | Wait for changes | `ifplugstatus -w` | Monitors cable status changes |

---

## 🌐 DNS Commands

### 🔍 nslookup - DNS Lookup

**Purpose**: Query DNS servers to resolve domain names and IP addresses.

```bash
# Basic usage
nslookup google.com
```
*Looks up IP address for google.com domain.*

#### 🚩 Essential Usage

| Operation | Description | Example | Usage |
|-----------|-------------|---------|-------|
| `nslookup domain` | Forward lookup | `nslookup google.com` | Gets IP for domain |
| `nslookup IP` | Reverse lookup | `nslookup 8.8.8.8` | Gets domain for IP |
| `nslookup domain server` | Use specific DNS | `nslookup google.com 8.8.8.8` | Query specific DNS server |
| `-type=record` | Query record type | `nslookup -type=MX google.com` | Query MX records |
| `-debug` | Debug mode | `nslookup -debug google.com` | Shows detailed query info |

### ⚡ dig - Advanced DNS Lookup

**Purpose**: Powerful and flexible DNS lookup tool with detailed output options.

```bash
# Basic usage
dig google.com
```
*Performs comprehensive DNS lookup for google.com.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `+short` | Short answer only | `dig +short google.com` | Shows only IP address |
| `@server` | Use specific DNS server | `dig @8.8.8.8 google.com` | Query Google's DNS |
| `-t type` | Query specific record | `dig -t MX google.com` | Query MX records |
| `-x` | Reverse lookup | `dig -x 8.8.8.8` | Reverse DNS lookup |
| `+trace` | Trace DNS path | `dig +trace google.com` | Shows complete resolution path |
| `+noall +answer` | Answer section only | `dig +noall +answer google.com` | Clean answer format |

---

## 📥 Data Transfer Commands

### 🌊 curl - Data Transfer Tool

**Purpose**: Transfer data to/from servers using various protocols (HTTP, HTTPS, FTP, etc.).

```bash
# Basic usage
curl https://google.com
```
*Downloads content from google.com.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-o filename` | Save to file | `curl -o page.html https://google.com` | Saves output to file |
| `-O` | Save with remote name | `curl -O https://example.com/file.zip` | Uses remote filename |
| `-L` | Follow redirects | `curl -L https://bit.ly/short-url` | Follows HTTP redirects |
| `-I` | Headers only | `curl -I https://google.com` | Shows HTTP headers only |
| `-v` | Verbose output | `curl -v https://google.com` | Shows detailed request/response |
| `-H "header"` | Custom header | `curl -H "User-Agent: MyApp" https://api.example.com` | Adds custom header |
| `-d data` | POST data | `curl -d "key=value" https://api.example.com` | Sends POST request |
| `-X method` | HTTP method | `curl -X DELETE https://api.example.com/item/1` | Uses DELETE method |

### 📦 wget - File Downloader

**Purpose**: Download files from web servers, supports recursive downloads and resume capability.

```bash
# Basic usage
wget https://example.com/file.zip
```
*Downloads file.zip from the specified URL.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-O filename` | Save with specific name | `wget -O myfile.zip https://example.com/file.zip` | Saves with custom name |
| `-c` | Continue partial download | `wget -c https://example.com/largefile.iso` | Resumes interrupted download |
| `-r` | Recursive download | `wget -r https://example.com/` | Downloads entire website |
| `-np` | No parent directories | `wget -r -np https://example.com/folder/` | Stays within folder |
| `-q` | Quiet mode | `wget -q https://example.com/file.zip` | Silent download |
| `--limit-rate` | Limit download speed | `wget --limit-rate=200k https://example.com/file.zip` | Limits to 200KB/s |
| `-t retries` | Set retry attempts | `wget -t 3 https://example.com/file.zip` | Retries 3 times on failure |

### 🔗 telnet - Remote Connection

**Purpose**: Establish remote connections to test network services and ports.

```bash
# Basic usage
telnet google.com 80
```
*Tests connectivity to google.com on port 80.*

#### 🚩 Essential Usage

| Usage | Description | Example | Purpose |
|-------|-------------|---------|---------|
| `telnet host port` | Test port connectivity | `telnet 192.168.1.1 22` | Tests SSH port |
| `telnet host` | Default telnet connection | `telnet server.example.com` | Connects to telnet service |
| `telnet smtp.server.com 25` | Test mail server | `telnet smtp.gmail.com 587` | Tests SMTP connectivity |
| `telnet ftp.server.com 21` | Test FTP server | `telnet ftp.example.com 21` | Tests FTP connectivity |

---

## 🛡️ Security & Monitoring Commands

### 🧱 iptables - Firewall Configuration

**Purpose**: Configure Linux kernel firewall rules for packet filtering and NAT.

```bash
# Basic usage
sudo iptables -L
```
*Lists all current firewall rules.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-L` | List rules | `sudo iptables -L` | Shows all chains and rules |
| `-A chain` | Append rule | `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT` | Allows SSH traffic |
| `-D chain rule` | Delete rule | `sudo iptables -D INPUT 1` | Deletes first INPUT rule |
| `-I chain pos` | Insert rule | `sudo iptables -I INPUT 1 -p tcp --dport 80 -j ACCEPT` | Inserts HTTP rule at position 1 |
| `-F` | Flush all rules | `sudo iptables -F` | Removes all rules |
| `-P chain policy` | Set default policy | `sudo iptables -P INPUT DROP` | Sets default INPUT to DROP |
| `-t table` | Specify table | `sudo iptables -t nat -L` | Shows NAT table rules |
| `-v` | Verbose output | `sudo iptables -L -v` | Shows detailed rule information |

### 👀 watch - Command Monitoring

**Purpose**: Execute commands repeatedly and display results in real-time.

```bash
# Basic usage
watch netstat -tuln
```
*Continuously monitors network connections, updating every 2 seconds.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-n seconds` | Set update interval | `watch -n 5 netstat -tuln` | Updates every 5 seconds |
| `-d` | Highlight differences | `watch -d netstat -tuln` | Highlights changes |
| `-t` | Turn off header | `watch -t date` | Hides title and timestamps |
| `-c` | Interpret color codes | `watch -c ls --color` | Shows colored output |
| `-x` | Exit on command failure | `watch -x ping -c 1 google.com` | Exits if ping fails |
| `-g` | Exit on output change | `watch -g ls /tmp` | Exits when output changes |

### 🗺️ nmap - Network Scanner

**Purpose**: Network discovery and security auditing tool for port scanning and host detection.

```bash
# Basic usage
nmap 192.168.1.1
```
*Scans common ports on the target host.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-p ports` | Scan specific ports | `nmap -p 22,80,443 192.168.1.1` | Scans SSH, HTTP, HTTPS ports |
| `-sS` | TCP SYN scan | `nmap -sS 192.168.1.1` | Stealth TCP scan |
| `-sU` | UDP scan | `nmap -sU 192.168.1.1` | Scans UDP ports |
| `-A` | Aggressive scan | `nmap -A 192.168.1.1` | OS detection, scripts, traceroute |
| `-O` | OS detection | `nmap -O 192.168.1.1` | Attempts OS fingerprinting |
| `-sn` | Ping scan only | `nmap -sn 192.168.1.0/24` | Host discovery without port scan |
| `-v` | Verbose output | `nmap -v 192.168.1.1` | Shows detailed scan progress |
| `-T timing` | Set timing template | `nmap -T4 192.168.1.1` | Uses aggressive timing |

### 🛣️ route - Routing Table Management

**Purpose**: Display and modify the IP routing table.

```bash
# Basic usage
route -n
```
*Displays the routing table with numerical addresses.*

#### 🚩 Essential Flags

| Flag | Description | Example | Usage |
|------|-------------|---------|-------|
| `-n` | Numerical addresses | `route -n` | Shows IPs instead of hostnames |
| `add` | Add route | `sudo route add -net 192.168.2.0/24 gw 192.168.1.1` | Adds network route |
| `del` | Delete route | `sudo route del -net 192.168.2.0/24` | Removes network route |
| `add default` | Add default gateway | `sudo route add default gw 192.168.1.1` | Sets default gateway |
| `-v` | Verbose output | `route -v` | Shows detailed routing info |
| `-C` | Show cache | `route -C` | Displays routing cache |
| `-F` | Show FIB | `route -F` | Shows forwarding information base |

---

## 💡 Quick Reference

### 🔥 Most Used Commands

```bash
# Network connectivity
ping -c 4 google.com                 # Test connectivity
traceroute google.com                # Trace network path
mtr google.com                       # Continuous monitoring

# Interface information
ip addr show                         # Modern interface info
ifconfig                            # Traditional interface info
ss -tuln                            # Active connections
netstat -tuln                       # Legacy connection info

# DNS operations
dig +short google.com               # Quick DNS lookup
nslookup google.com                 # Interactive DNS lookup

# Network scanning
nmap -sn 192.168.1.0/24            # Network discovery
nmap -p 1-1000 192.168.1.1         # Port scanning

# File operations
curl -O https://example.com/file.zip # Download with curl
wget https://example.com/file.zip    # Download with wget
```

### 🎯 Troubleshooting Workflow

```bash
# 1. Check local interface
ip addr show

# 2. Test local connectivity
ping -c 3 127.0.0.1

# 3. Test gateway
ping -c 3 $(ip route | grep default | awk '{print $3}')

# 4. Test external connectivity
ping -c 3 8.8.8.8

# 5. Test DNS resolution
dig +short google.com

# 6. Trace network path
traceroute google.com

# 7. Check listening services
ss -tuln
```

---

## 🔧 Installation

Most commands are pre-installed on Linux systems. For missing tools:

### Ubuntu/Debian
```bash
sudo apt update
sudo apt install net-tools dnsutils traceroute mtr-tiny nmap curl wget telnet iputils-ping
```

### CentOS/RHEL/Fedora
```bash
sudo yum install net-tools bind-utils traceroute mtr nmap curl wget telnet iputils
# or for newer versions:
sudo dnf install net-tools bind-utils traceroute mtr nmap curl wget telnet iputils
```

### Arch Linux
```bash
sudo pacman -S net-tools bind-tools traceroute mtr nmap curl wget inetutils
```

---

## 📚 Additional Resources

### 📖 Documentation Links
- [Linux Network Commands Manual](https://linux.die.net/man/)
- [TCP/IP Networking Fundamentals](https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13769-5.html)
- [Network Troubleshooting Guide](https://tldp.org/LDP/nag2/x-087-2-troubleshooting.html)

### 🛠️ Related Tools
- **Advanced**: `tcpdump`, `wireshark`, `iftop`, `nethogs`
- **Monitoring**: `vnstat`, `bandwidthd`, `ntopng`