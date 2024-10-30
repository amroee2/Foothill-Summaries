# Proxy

A proxy server is a system or router that provides a gateway between users and the internet. Therefore, it helps prevent cyber attackers from entering a private network. It is a server, referred to as an “intermediary” because it goes between end-users and the web pages they visit online.

When a computer connects to the internet, it uses an IP address. This is similar to your home’s street address, telling incoming data where to go and marking outgoing data with a return address for other devices to authenticate. A proxy server is essentially a computer on the internet that has an IP address of its own.

Proxies provide a valuable layer of security for your computer. They can be set up as web filters or firewalls, protecting your computer from internet threats like malware.

This extra security is also valuable when coupled with a secure web gateway or other email security products. This way, you can filter traffic according to its level of safety or how much traffic your network—or individual computers—can handle.

![image](https://github.com/user-attachments/assets/0df961bb-ce8f-4e07-92f7-204711b4d89a)

## Benefits

- Enhanced security: Can act like a firewall between your systems and the internet. Without them, hackers have easy access to your IP address, which they can use to infiltrate your computer or network.

- Private browsing, watching, listening, and shopping: Use different proxies to help you avoid getting inundated with unwanted ads or the collection of IP-specific data. With a proxy, site browsing is well-protected and impossible to track.

- Access to location-specific content: You can designate a proxy server with an address associated with another country. You can, in effect, make it look like you are in that country and gain full access to all the content computers in that country are allowed to interact with. For example, the technology can allow you to open location-restricted websites by using local IP addresses of the location you want to appear to be in.

- Prevent employees from browsing inappropriate or distracting sites: You can use it to block access to websites that run contrary to your organization’s principles. Also, you can block sites that typically end up distracting employees from important tasks. Some organizations block social media sites like Facebook and others to remove time-wasting temptations.

## Types Of Proxy Server

**Forward Proxy**

A forward proxy sits in front of clients and is used to get data to groups of users within an internal network. When a request is sent, the proxy server examines it to decide whether it should proceed with making a connection.

A forward proxy is best suited for internal networks that need a single point of entry. It provides IP address security for those in the network and allows for straightforward administrative control. However, a forward proxy may limit an organization’s ability to cater to the needs of individual end-users.

**Reverse Proxy**

Unlike a forward proxy, which sits in front of clients, a reverse proxy is positioned in front of web servers and forwards requests from a browser to the web servers. It works by intercepting requests from the user at the network edge of the web server. It then sends the requests to and receives replies from the origin server.

Reverse proxies are a strong option for popular websites that need to balance the load of many incoming requests. They can help an organization reduce bandwidth load because they act like another web server managing incoming requests. The downside is reverse proxies can potentially expose the HTTP server architecture if an attacker is able to penetrate it. This means network administrators may have to beef up or reposition their firewall if they are using a reverse proxy.

**A forward proxy deals with client traffic, regulating and securing it. In contrast, a reverse proxy shields servers by handling client requests, ensuring they reach the right server, and returning the results to clients, who are unaware of the server's direct involvement.**


# VPN

VPN stands for "Virtual Private Network" and describes the opportunity to establish a protected network connection when using public networks. VPNs encrypt your internet traffic and disguise your online identity. This makes it more difficult for third parties to track your activities online and steal data. The encryption takes place in real time.

A VPN hides your IP address by letting the network redirect it through a specially configured remote server run by a VPN host. This means that if you surf online with a VPN, the VPN server becomes the source of your data. This means your Internet Service Provider (ISP) and other third parties cannot see which websites you visit or what data you send and receive online. A VPN works like a filter that turns all your data into "gibberish". Even if someone were to get their hands on your data, it would be useless.

## Benefits

- Secure encryption: To read the data, you need an encryption key . Without one, it would take millions of years for a computer to decipher the code in the event of a brute force attack . With the help of a VPN, your online activities are hidden even on public networks.

- Disguising your whereabouts : VPN servers essentially act as your proxies on the internet. Because the demographic location data comes from a server in another country, your actual location cannot be determined. In addition, most VPN services do not store logs of your activities. Some providers, on the other hand, record your behavior, but do not pass this information on to third parties. This means that any potential record of your user behavior remains permanently hidden.

- Access to regional content: Regional web content is not always accessible from everywhere. Services and websites often contain content that can only be accessed from certain parts of the world. Standard connections use local servers in the country to determine your location. This means that you cannot access content at home while traveling, and you cannot access international content from home. With VPN location spoofing , you can switch to a server to another country and effectively “change” your location.

- Secure data transfer: If you work remotely, you may need to access important files on your company’s network. For security reasons, this kind of information requires a secure connection. To gain access to the network, a VPN connection is often required. VPN services connect to private servers and use encryption methods to reduce the risk of data leakage.


# Network Load Balancer

Load Balancers are in charge of distributing the traffic comming from user requests into multiple servers, depending on the load balancer used, it can have a lot of benefits.

Some load balancers can automatically decide how to distribute user requests to servers, and which ones to use. If 2 servers are used up until 90% utilization, it can automatically decide to forward traffic to a third server, or only use 1 server when there isnt much traffic, to minimize cost.

## Load balancers algorithms

**Dumb Load Balancer**

Some load balancers use **round robin**, it distributes traffic uniformly, gives the first server a client, then the 2nd, then the 3rd....

This has several disadvantages with the main one being that its not consistent or "fair". The first and fourth use could spend hours on the application whilst the 2nd and 3rd could spend minutes, this puts pressure on the first server while the 2nd and 3rd are free.

**Smart Load Balancer**

Instead of the load balancer acting as a king and distributing traffic to servers without the needed information like utilization percentage, smart load balancers communicate with the servers and work in cooperation, the notify the load balancers of their trafic and resources consumption, and then the load balancer decides which server is most suitable for a new client when they arrive.

**Average Load Balancer**

This load balancer comes in the middle, its works better than the dumb load balancer but it doesnt have all the setup and configs for the smart one, it picks a certain algorithm (there are almost 10 different ones) to assign traffic for servers, one algorithm can use a randomizing function.
