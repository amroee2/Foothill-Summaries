# Client - Server Model

The Client-server model is a distributed application structure that partitions tasks or workloads between the providers of a resource or service, called servers, and service requesters called clients. In the client-server architecture, when the client computer sends a request for data to the server through the internet, the server accepts the requested process and delivers the data packets requested back to the client. Clients do not share any of their resources. Examples of the Client-Server Model are Email, World Wide Web, etc.

## How does this model work?

Client: When we say the word Client, it means to talk of a person or an organization using a particular service. Similarly in the digital world, a Client is a computer (Host) i.e. capable of receiving information or using a particular service from the service providers (Servers).

Servers: Similarly, when we talk about the word Servers, It means a person or medium that serves something. Similarly in this digital world, a Server is a remote computer that provides information (data) or access to particular services.

![image](https://github.com/user-attachments/assets/a734f870-3436-4e68-9e57-50ab11e7afb6)

# How the Browser Interacts With the Servers?

- User enters the URL(Uniform Resource Locator) of the website or file. The Browser then requests the DNS(DOMAIN NAME SYSTEM) Server.

- DNS Server lookup for the address of the WEB Server.

- The DNS Server responds with the IP address of the WEB Server.
  
- The Browser sends over an HTTP/HTTPS request to the WEB Server’s IP (provided by the DNS server).

- The Server sends over the necessary files for the website.

- The Browser then renders the files and the website is displayed. This rendering is done with the help of DOM (Document Object Model) interpreter, CSS interpreter, and JS Engine collectively known as the JIT or (Just in Time) Compilers.

![image](https://github.com/user-attachments/assets/bbb8ee84-61b7-416c-a748-0cebc4b26380)

## Advantages of Client-Server Model

- Centralized system with all data in a single place.
- Cost efficient requires less maintenance cost and Data recovery is possible.
- The capacity of the Client and Servers can be changed separately.

## Disadvantages of Client-Server Model

- Clients are prone to viruses, Trojans, and worms if present in the Server or uploaded into the Server.
- Servers are prone to Denial of Service (DOS) attacks.
- Data packets may be spoofed or modified during transmission.
- Phishing or capturing login credentials or other useful information of the user are common and MITM(Man in the Middle) attacks are common.

# Ports

A port is a logical connection used by different programs and services to exchange informations, through it we can specifically determine which type of service is going to be used (Web page, Email, file transfer...).

All ports have unique numbers, ranging from 0 - 65535.

## Common Port Numbers

- HTTPS -> 443
- HTTP -> 80
- Email (SMTP) -> 25
- File tranfer (FTP) -> 21

Ports are always associated with an **IP address**, through the IP address we can find the location of the server, and through the port number we can identify which **service** we want from that server.

Through ```netstat -n``` on terminal, we can check our current active connections.

Our local ip address represents our location, associated with the free temporary port number given to us

Foreign addresses are the current active connections, like google servers and other servers as well.

## Ports categories

- System / Well Known Ports:

They range from 0 - 1023, they represent the commonly used services (web pages, email, file transfer) like the ones mentioned above

- User / Registred Ports:

They range from 1024 - 49151, they are ports registred by companies/developers for a particular service

1102 - Adobe Server
1433 - Microsoft SQL Server
1527 - Oracle

- Dynamic / Private Ports:

They range from 49152 - 65535, they are ports that our computer assigns temporarily to itself during a session, you can see that number changes a lot when calling ```netstat -n```

