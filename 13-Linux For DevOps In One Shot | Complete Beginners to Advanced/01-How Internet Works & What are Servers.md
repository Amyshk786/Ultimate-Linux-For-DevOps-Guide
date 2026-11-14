# Day 1 – Computer Networking, Internet, Servers and Boot Process

These notes cover the fundamentals of computer networking, how the Internet works, data transmission, servers, web servers, application servers, applications and the Linux boot process.

---

# 1. What is Computer Networking?

Let's understand networking with a simple example.

Suppose:
- You are in Pune, India.
- Your friend is in Kashmir, India.
- Another friend is in New York, USA.

### Standalone Computer

When a computer is not connected to any other computer through a network, it can be called a standalone computer.

Example:

```text
Computer A

(Standalone)
```

A standalone computer can still use its own installed applications and files.

### Computer Network

When two or more computers are connected and can communicate with each other, it is called a computer network.

Example:

```text
Computer A  <------>  Computer B
     |
     |
Computer C
```

Computers can communicate and share resources such as:
- Files
- Printers
- Applications
- Data
- Network services

### Internet

When networks around the world are interconnected, they form the Internet.

For example:

```text
Pune Network
     |
     |
     +------------------+
                        |
                   The Internet
                        |
     +------------------+
     |
     |
Kashmir Network

     |
     |
New York Network
```

The Internet is a global network of interconnected networks that communicate using standard protocols such as TCP/IP.

**Remember:**
- Standalone computer – Not connected to another computer through a network.
- Computer network – Two or more connected devices.
- Internet – A worldwide network of interconnected networks.

---

# 2. How Does the Internet Work?

The Internet uses a combination of physical infrastructure, networking devices, service providers and communication protocols.

One important part of this infrastructure is fiber-optic cable.

## A. Worldwide Connectivity – Submarine Fiber-Optic Cables

<escape> </escape>

Fiber-optic cables carry data using light signals.

Submarine fiber-optic cables are installed under the sea and connect countries and continents.

They carry a significant amount of international Internet traffic.

Examples of infrastructure:
- Submarine cables
- International data centers
- Internet service provider networks
- Telecom carrier networks

**Important:** The Internet does not depend only on submarine cables. It also uses terrestrial fiber, wireless links, satellite connectivity and other networking infrastructure.

## B. Country-Level Connectivity – WAN

WAN stands for **Wide Area Network**.

A WAN connects networks across large geographical areas, such as:
- Different cities
- Different states
- Different countries

Telecom operators and network providers use WAN infrastructure to connect their networks over long distances.

Examples include:
- Carrier networks
- MPLS networks
- Long-distance fiber networks
- Private enterprise WANs

## C. City-Level Connectivity – MAN and IXP

**MAN – Metropolitan Area Network**

A MAN connects networks across a city or metropolitan area.

For example, a telecom operator may use fiber infrastructure to connect multiple areas of Pune.

**IXP – Internet Exchange Point**

An IXP is a physical interconnection facility where different Internet networks connect and exchange traffic.

For example:
- ISP networks
- Telecom operators
- Content delivery networks
- Cloud and content providers

An IXP allows participating networks to exchange traffic directly instead of sending all traffic through another network provider.

**Important:** An IXP is not simply a data center that gives Internet to ISPs. It is an interconnection point where networks establish peering connections.

## D. Home-Level Connectivity – LAN

**LAN – Local Area Network**

A LAN connects devices within a limited geographical area, such as:
- Home
- Office
- School
- Data center

Example:

```text
                Internet
                    |
                ISP Network
                    |
               Home Router
                    |
              Wi-Fi / Ethernet
             /       |       \
          Laptop   Mobile    Desktop
```

Examples of Internet Service Providers in India:
- Airtel
- Jio
- Hathway
- Local broadband providers

The ISP provides Internet connectivity to your home or office.

Your router distributes that connection to devices through Wi-Fi or Ethernet.

**Remember:**

| Network | Full Form | Coverage |
|---|---|---|
| LAN | Local Area Network | Home, office or building |
| MAN | Metropolitan Area Network | City |
| WAN | Wide Area Network | Large geographical areas |

---

# 3. How Is Data Transferred Over the Internet?

When you send data from one computer to another, the data is divided into smaller units for transmission.

These units are commonly called **packets**.

A packet is a formatted unit of data transmitted across a network from a source to a destination.

For example, when you open YouTube:
1. Your device sends a request.
2. The request travels through your local network and ISP.
3. Routers forward the packets toward their destination.
4. YouTube's infrastructure processes the request.
5. Response data travels back to your device.
6. Your browser displays the content.

Simplified flow:

```text
Your Laptop
     |
     v
Home Router
     |
     v
ISP Network
     |
     v
Internet Routers
     |
     v
YouTube Infrastructure
     |
     v
Response to Your Laptop
```

Packets contain control information such as source and destination addresses, along with the data being transported.

---

# 4. Important Networking Terms

## A. Latency

Latency is the time taken for data to travel from a source to a destination.

Example:

You send a request to a server in New York from Pune.

If the network round-trip takes 200 milliseconds, the round-trip latency is approximately 200 ms.

**Lower latency generally means faster response time.**

## B. Bandwidth

Bandwidth is the maximum amount of data that a network connection can transfer in a given amount of time.

It is generally measured in:
- Kbps – Kilobits per second
- Mbps – Megabits per second
- Gbps – Gigabits per second

Example:

If your Internet connection has a bandwidth of 100 Mbps, its theoretical maximum transfer rate is 100 megabits per second.

**Important:** Mbps and MBps are different.

- Mbps = Megabits per second.
- MBps = Megabytes per second.
- 8 bits = 1 byte.

## C. Jitter

Jitter is the variation in packet delay over time.

Example:

Suppose packets arrive with these delays:

```text
Packet 1 = 20 ms
Packet 2 = 25 ms
Packet 3 = 60 ms
Packet 4 = 30 ms
```

The variation in delay is an example of jitter.

High jitter can affect:
- Video calls
- Online gaming
- Voice calls
- Live streaming

## D. Packet Loss

Packet loss occurs when packets sent across a network fail to reach their destination.

Example:

Suppose you send 100 packets, but only 95 arrive.

```text
Total packets sent     = 100
Packets received       = 95
Packets lost           = 5
Packet loss            = 5%
```

Packet loss can cause:
- Slow application performance
- Video buffering
- Audio interruptions
- Network communication problems

**DevOps use case:** Latency, bandwidth, jitter and packet loss are important metrics when troubleshooting application and network performance.

---

# 5. What Are Servers?

A server is a computer system or software program that provides services, resources or data to other computers called clients.

Examples:
- Web server
- Application server
- Database server
- File server
- DNS server
- Mail server

### Client-Server Architecture

A client sends a request, and a server processes the request and returns a response.

Example:

```text
       Client
      (Browser)
          |
          | HTTP Request
          v
        Server
          |
          | HTTP Response
          v
       Client
      (Browser)
```

Example:

When you open Facebook:
1. You open the website in your browser.
2. The browser sends a request to Facebook's infrastructure.
3. The server-side application processes the request.
4. The application may communicate with databases and other services.
5. The server returns a response.
6. Your browser displays the page.

### Types of Servers

| Server | Purpose |
|---|---|
| Web Server | Handles HTTP requests and serves web content |
| Application Server | Runs application logic |
| Database Server | Stores and manages data |
| File Server | Stores and shares files |
| DNS Server | Resolves domain names into IP addresses |
| Mail Server | Sends and receives email |

### Reference Material

Additional Linux learning material:

[TWS – Linux for DevOps PDF](https://d502jbuhuh9wk.cloudfront.net/digital_products/62cd128e0cf2e6a1694683bb/66e675e1ec05f81ffc9b0c8f/asset/1726379489324/file.pdf)

---

# 6. Difference Between Web Server and Application Server

## A. Web Server

A web server is software that handles HTTP/HTTPS requests and serves web content to clients.

It commonly serves:
- HTML
- CSS
- JavaScript
- Images
- Static files

Examples:
- Nginx
- Apache HTTP Server
- Microsoft IIS

A web server can also act as a reverse proxy and forward requests to application servers.

Example:

```text
Browser
   |
   | HTTP Request
   v
Nginx Web Server
   |
   v
Static HTML / CSS / Images
```

## B. Application Server

An application server provides an environment for running application code and processing business logic.

It can:
- Process user requests
- Execute application logic
- Communicate with databases
- Generate dynamic responses
- Integrate with other services

Examples of application technologies and runtimes:
- Node.js applications
- Django applications served using Gunicorn or Uvicorn
- Java applications running on Tomcat

**Important:** Node.js and Django are application technologies/runtimes or frameworks, not necessarily standalone application-server products. Gunicorn, Uvicorn and Tomcat are examples of servers used to run application code.

### Web Server vs Application Server

| Web Server | Application Server |
|---|---|
| Handles HTTP requests and serves web content | Runs application logic |
| Commonly serves static files | Commonly generates dynamic responses |
| Can act as a reverse proxy | Processes business operations |
| Example: Nginx, Apache | Example: Tomcat, Gunicorn, Uvicorn |

### Real-World Example

Suppose a user opens an e-commerce website.

```text
              User Browser
                   |
                   v
              Nginx Server
                   |
                   v
           Application Server
             (Django App)
                   |
                   v
             Database Server
                   |
                   v
              Response
```

Here:
- Nginx receives the HTTP request.
- Django executes the business logic.
- The database provides product or customer information.
- The response is sent back through Nginx to the browser.

---

# 7. Difference Between Web Application and Standalone Application

## A. Standalone Application

A standalone application is software installed and executed directly on a user's computer.

It does not necessarily require an Internet connection or a remote server for its core functionality.

Examples:
- Calculator
- Notepad
- VLC Media Player
- Offline desktop word processors

Some desktop applications may still require Internet connectivity for updates, synchronization or online features.

## B. Web Application

A web application is accessed through a web browser over a network.

Examples:
- Facebook
- YouTube
- Amazon
- eBay
- Google Docs

A typical web application uses:
- Frontend
- Backend
- Database
- Web server
- Application server

### Standalone vs Web Application

| Standalone Application | Web Application |
|---|---|
| Installed and executed on a local device | Accessed through a web browser |
| Can work offline | Usually requires network connectivity |
| May store data locally | Often communicates with remote servers |
| Updates may need local installation | Updates are commonly deployed centrally |
| Example: VLC | Example: YouTube |

**Important:** Some modern web applications support offline functionality using technologies such as service workers and browser storage.

---

# 8. What Is a Boot Loader?

A boot loader is a software component responsible for loading the operating system kernel into memory and starting the operating system.

When you switch on a computer, the operating system is not immediately running.

The system must go through a boot process.

### Basic Linux Boot Process

```text
       Power On
           |
           v
      BIOS / UEFI
           |
           v
    Boot Manager
           |
           v
       Boot Loader
           |
           v
    Linux Kernel
           |
           v
       initramfs
           |
           v
    Root Filesystem
           |
           v
     systemd (PID 1)
           |
           v
   Services and Login
```

The exact sequence can vary depending on the firmware, boot configuration and Linux distribution.

## A. BIOS / UEFI

BIOS and UEFI are firmware interfaces that initialize the hardware and start the boot process.

- BIOS – Traditional firmware interface.
- UEFI – Modern firmware interface.

## B. Boot Manager

The boot manager selects which operating system or boot entry should be started.

For example, a computer with multiple operating systems may allow the user to select which OS to boot.

## C. Boot Loader

The boot loader loads the operating system kernel into memory.

It may also load the initial RAM filesystem (initramfs) and pass boot parameters to the kernel.

## D. Linux Kernel

The kernel is the core component of the Linux operating system.

It manages:
- CPU
- Memory
- Processes
- Devices
- Filesystems
- Hardware communication

## E. initramfs

The initial RAM filesystem provides temporary tools and modules needed during early boot.

It helps the kernel locate and mount the actual root filesystem.

## F. systemd

On many modern Linux distributions, systemd is the first userspace process and runs as PID 1.

It starts and manages system services and other units.

---

# 9. Tasks Performed by a Boot Loader

A typical boot loader performs tasks such as:

1. Loading and interpreting boot configuration.
2. Allowing the selection of a boot entry or kernel.
3. Loading the Linux kernel into memory.
4. Loading the initial RAM filesystem, if configured.
5. Passing boot parameters to the kernel.
6. Transferring control to the kernel.

**Important:** The Linux kernel is responsible for much of the subsequent hardware initialization, driver initialization, filesystem mounting and userspace startup. These are not all tasks performed by the boot loader.

---

# 10. Examples of Boot Loaders

### 1. GRUB – Grand Unified Bootloader

GRUB is a widely used boot loader in Linux systems.

It supports:
- Booting Linux kernels
- Multiple operating systems
- Multiple kernel versions
- Boot configuration options

### 2. LILO – Linux Loader

LILO is an older Linux boot loader.

It was historically used in Linux distributions but has largely been replaced by GRUB.

### 3. Windows Boot Manager

Windows Boot Manager is used by Windows systems to select and start a Windows boot environment.

---

# 11. Important DevOps Interview Questions

1. What is a standalone computer?
2. What is computer networking?
3. What is the Internet?
4. What is the difference between LAN, MAN and WAN?
5. What is an Internet Exchange Point?
6. What are submarine fiber-optic cables?
7. How does data travel from one computer to another?
8. What is a network packet?
9. What is latency?
10. What is bandwidth?
11. What is jitter?
12. What is packet loss?
13. What is a server?
14. What is client-server architecture?
15. What is the difference between a web server and an application server?
16. What is the difference between a web application and a standalone application?
17. What is Nginx?
18. What is the purpose of an application server?
19. What is a boot loader?
20. What is the difference between BIOS and UEFI?
21. Explain the Linux boot process.
22. What is GRUB?
23. What is the Linux kernel?
24. What is initramfs?
25. What is systemd?

---

# 12. Real-World DevOps Connection

Understanding these fundamentals helps DevOps engineers troubleshoot infrastructure and application issues.

| Concept | DevOps Application |
|---|---|
| LAN / WAN | Understand network connectivity |
| Fiber-optic infrastructure | Understand the physical Internet backbone |
| Packets | Understand network communication |
| Latency | Troubleshoot slow application responses |
| Bandwidth | Identify network capacity limitations |
| Jitter | Troubleshoot real-time communication issues |
| Packet loss | Investigate unreliable network connections |
| Web Server | Configure Nginx and Apache |
| Application Server | Deploy Django, Node.js and Java applications |
| Standalone Application | Understand locally installed software |
| Boot Loader | Understand how Linux starts |
| Linux Kernel | Understand operating system fundamentals |
| systemd | Manage Linux services |

---

## Day 1 – Learning Outcome

After completing this topic, you should understand:

- What standalone computers and computer networks are.
- How the Internet connects different networks around the world.
- What LAN, MAN, WAN and IXP mean.
- How data is transferred using packets.
- The difference between latency, bandwidth, jitter and packet loss.
- What servers do and how client-server architecture works.
- The difference between web servers and application servers.
- The difference between standalone and web applications.
- How a Linux machine boots from firmware to userspace.
- The role of GRUB, the Linux kernel, initramfs and systemd.

**Next recommended topic:** IP Addressing – IPv4 vs IPv6, Public IP vs Private IP, Static IP vs Dynamic IP and Subnetting.
