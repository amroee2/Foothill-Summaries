# HTTP

HTTP (HyperText Transfer Protocol) is a stateless, application-layer protocol used for transmitting hypermedia documents, such as HTML. It is the foundation of any data exchange on the Web and follows a client-server model where a web browser (client) sends requests to a web server, which responds with the requested resources.

![image](https://github.com/user-attachments/assets/00e91cbc-2f05-4405-97bc-d63af6898e07)

HTTP works as a request-response protocol. The client (usually a web browser) sends an HTTP request to the server, which processes the request and returns an HTTP response.

Key Characteristics:

- Stateless: Each request is independent.
- Text-based protocol: Both the request and response messages are in plain text, making it human-readable and easy to debug.
- Client-server model: The client initiates requests, and the server responds with the appropriate resources.

![image](https://github.com/user-attachments/assets/b4a7cf44-04dc-43e2-abaa-28b358018559)

URL (Uniform Resource Locator): Defines the address of a web resource. A URL typically consists of:

- http://: The protocol (HTTP or HTTPS)

- www.example.com: The domain name (or IP address)
  
- /index.html: The specific resource requested

Default Ports:

Port 80 for HTTP
Port 443 for HTTPS (secure version of HTTP with encryption)

**Http methods**

![image](https://github.com/user-attachments/assets/c6c0b606-54bf-43a0-93ae-1d3153f680df)

**Htpp status codes**

![image](https://github.com/user-attachments/assets/98eeb803-371a-4cc4-bee5-2023537d8b8c)

## HTTPS

Hypertext transfer protocol secure (HTTPS) is the secure version of HTTP, which is the primary protocol used to send data between a web browser and a website. HTTPS is encrypted in order to increase security of data transfer.


## HTTP Request Structure

- Request line: Specifies the method, resource URL, and HTTP version.

- Additional information about the request, like metadata and control information.

```
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html
```

- Body (Optional): Contains data sent to the server, typically in POST or PUT requests

## HTTP Response Structure

- Status Line: Contains the HTTP version, status code, and status message.

- Headers: Additional information about the response.

```
Content-Type: text/html
Content-Length: 348
Set-Cookie: sessionId=abc123; HttpOnly
```

- Body (Optional): Contains the requested resource (e.g., HTML, JSON data).
