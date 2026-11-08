
Suppose you are in Pune, your friend is in Kashmir, and your other friend is in New York

-> When your computer is not connected to any other computer, then it is called a Standalone

-> If all your computers are connected, then it is called Computer Networking [A, B & C are connected to each other]

-> When all these Devices are Inter-Connected then it is called the Internet.

-> Internet flows through Fiber Optic Cables




# How the Internet Works

-> World - Across the world, we have Fiber Optic Cables, which are in the sea.

-> Country - In the Country, various Companies have purchased these Fiber Optic Cables Wide Area Network (WAN)

-> City - The Data is then transmitted from these Fiber Optic Cables to a City Metropolitan Area Network (MAN),  an Internet Exchange Point (IXP), which is a physical data center. [IXP gives Internet to ISP]

-> Home - The ISP takes Internet from IXP and provides us Internet in the form of WiFi, which is a Local Area Network (LAN) [U-Broadband, Airtel, Jio, Hathway]




# This Data is Transferred in Packets from One Computer to another 

[A packet is a formatted unit of data that is transmitted across a computer network from a source to a destination. The data is encoded]

[Latency is the time it takes for data to travel from a source to a destination across a network.]

[Bandwidth is the maximum amount of data that can be transmitted over a network connection in a given amount of time.]

[Jitter is the variation in the delay (latency) of data packets as they travel across a network.]

[Packet loss is when some pieces of data sent over a network fail to reach their destination.] Imagine you're sending 100 messages over the internet, but only 95 arrive. The other 5 are lost along the way. That's 5% packet loss.








# What are Servers?

Notes Provided by TWS For Linux - https://d502jbuhuh9wk.cloudfront.net/digital_products/62cd128e0cf2e6a1694683bb/66e675e1ec05f81ffc9b0c8f/asset/1726379489324/file.pdf


# Difference Between Web Server and Application Server
-------------------------------------------------------



# Web Server - A Web Server is a computer program or device that serves web content, primarily hosting websites and handling HTTP requests from clients (usually web browsers). It accepts requests for data and sends the specified documents, primarily static content such as HTML, CSS, and images.

-> Web Server per Static Data Rehta hai like Nginx, Apache HTTP Server





# Application Server - An Application Server provides a more comprehensive environment for running enterprise applications. It includes both a web container and an EJB (Enterprise JavaBeans) container, supporting a wide range of applications, including dynamic content and complex business operations.

-> Application Server per Dynamic data rhta h like Noje.js & Django Apps









# Difference Between Web Application and Standalone Application
----------------------------------------------------------------




# Standalone Application - A standalone application, also known as a desktop application, is a software program designed in such a way that to run this software program, users don't need an internet connection or any server access.

-> Standalone Applications are Like Calculator, Notepad, VLC Media Player, Microsoft Word





# Web Application - Web-based applications need an internet connection, servers, and any additional resources to run, but standalone applications do not require any additional resources, such as an internet connection, server, etc.

-> Web Applications are like Facebook, Twitter, YouTube, Amazon, eBay






# Boot Loader - Boot Loader is a software program that is responsible for "actually loading" the operating system once the Boot Manager has finished its work. And by loading the Operating System, we mean "loading the kernel of the Operating System".  The Boot Loader is typically a part of the Operating System itself. Till the point Boot Loader starts loading the OS, there is nothing in the Main Memory of the machine.





# Following are a series of tasks that a typical Boot Loader is expected to perform - 

1) Loading and parsing the Boot Configuration File.

2) Loading and initializing the OS's kernel into the main memory.

3) Loading and initializing the other system components and system drivers.

4) Finally, finish up the system environment setup and transfer the control to the kernel.







# Some examples of Boot Loaders are -

1) LILO (Linux Loader): Most popular Boot Loader for Linux - Based Machines

2) Windows Boot Loader: Specific to Windows Machines

3) Grand Unified Boot Loader GRUB (Boot Loader part): It is a sub-part of GRUB Boot Manager.
