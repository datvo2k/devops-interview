
#### Protocol questions?

###### What is HTTP?
HTTP stands for Hypertext Transfer Protocol. It is a set of rule which is used for transferring the files like audio, video, graphic image, text and other multimedia files on the WWW. HTTP is a protocol that is used to transfer the hypertext from the client end to the server end but not security. 

###### What are HTTP Request Messages?
HTTP Requests are messages which are sent by the client or user to initiate an action on the server.
It consists of various things:

a. Request Line: The Request-Line starts with a method token, which is followed by the Request-URI, the protocol version, and ending with CRLF. Using the SP characters, the elements are separated.

Syntax
Request-Line = Method SP Request-URI SP HTTP-Version CRLF

b. The Resource Identified by a Request:

c. Request Header Fields:The request-header fields are used to allow the client to pass additional information to the server like the request and the client itself. The request header fields act as request modifiers, with semantics equivalent to the parameters on a programming language method invocation.

###### What is HTTPS?
HTTPS stands for Hypertext Transfer Protocol Secure. HTTPS has a secure transfer. HTTPS is used to encrypt or decrypt user HTTP page or HTTP page requests that are returned by the web server.

###### What do you understand by TCP/IP?
TCP/IP is short for Transmission Control Protocol /Internet protocol. It is a set of protocol layers that is designed for exchanging data on different types of networks.

###### How many layers are in TCP/IP?
There are basic 4 layers in TCP/IP:
1. Application Layer
2. Transport Layer
3. Internet Layer
4. Network Layer


#### Docker questions?
###### Why and when do we use Docker?
1. Isolation: Docker containers provide isolation for applications and their dependencies, making it easier to deploy and run the same application consistently across different environments.

2. Portability: Docker containers can run on any host with the Docker engine installed, making it easy to move an application between development, staging, and production environments.

3. Scalability: Docker allows you to easily scale up or down the number of containers running an application, making it easy to handle changes in load or traffic.

4. Versioning: Docker allows you to version control your application, as well as the dependencies and configuration.

5. Efficient resource usage: Docker containers use fewer resources than traditional virtual machines, making them more efficient to run on the same host.

6. Microservices: Docker makes it easier to implement and manage a microservices architecture, allowing you to break down a monolithic application into smaller, loosely-coupled services.

###### What is Docker Life Cycle?
The lifecycle of a Docker container involves creation, running, stopping, and removal. Containers are created from Docker images, run as isolated instances, can be stopped or paused, and can be removed when no longer needed.