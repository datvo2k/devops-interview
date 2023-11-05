
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

###### What are some key features of a container?
Containers are isolated from each other and the underlying host operating system. This allows for consistent runtime environments and makes it easy to package and deploy applications. Containers are also lightweight and fast, making them ideal for microservices and other distributed applications.

###### What are different types of Docker Networking drivers?
Bridge: The default network driver. If you don’t specify a driver, this is the type of network you are creating. Bridge networks are usually used when your applications run in standalone containers that need to communicate.

Host: For standalone containers, remove network isolation between the container and the Docker host, and use the host’s networking directly. host is only available for swarm services on Docker 17.06 and higher.

Overlay: Overlay networks connect multiple Docker daemons together and enable swarm services to communicate with each other. You can also use overlay networks to facilitate communication between a swarm service and a standalone container, or between two standalone containers on different Docker daemons. This strategy removes the need to do OS-level routing between these containers. See overlay networks.

MacVLAN: Macvlan networks allow you to assign a MAC address to a container, making it appear as a physical device on your network. The Docker daemon routes traffic to containers by their MAC addresses. Using the macvlan driver is sometimes the best choice when dealing with legacy applications that expect to be directly connected to the physical network, rather than routed through the Docker host’s network stack.

None: For this container, disable all networking. Usually used in conjunction with a custom network driver. none is not available for swarm services.

###### How is overlay network different from bridge network?
Bridge networks connect two networks while creating a single aggregate network from multiple communication networks or network segments, hence the name bridge. Overlay networks are usually used to create a virtual network between two separate hosts. Virtual, since the network is build over an existing network. Bridge networks can cater to single host, while overlay networks are for multiple hosts.

###### Can you explain different volume mount types available in Docker?
There are three mount types available in Docker · Volumes are stored in a part of the host filesystem which is managed by Docker (/var/lib/docker/volumes/ on Linux). Non-Docker processes should not modify this part of the filesystem. Volumes are the best way to persist data in Docker. · Bind mounts may be stored anywhere on the host system. They may even be important system files or directories. Non-Docker processes on the Docker host or a Docker container can modify them at any time. · tmpfs mounts are stored in the host system’s memory only, and are never written to the host system’s filesystem.

###### Why do my services take 10 seconds to recreate or stop?
Compose stop attempts to stop a container by sending a SIGTERM. It then waits for a default timeout of 10 seconds. After the timeout, a SIGKILL is sent to the container to forcefully kill it. If you are waiting for this timeout, it means that your containers aren’t shutting down when they receive the SIGTERM signal.

###### Explain Docker Architecture?
- Docker Client: This performs Docker build pull and run operations to establish communication with the Docker Host. The Docker command uses Docker API to call the queries to be run.
- Docker Host: This component contains Docker Daemon, Containers and its images. The images will be the kind of metadata for the applications which are containerized in the containers. The Docker Daemon establishes a connection with Registry.
- Registry: This component will be storing the Docker images. The public registries are Docker Hub and Docker Cloud which can be s used by anyone.

###### What is the lifecycle of a Docker Container?
Docker containers have the following lifecycle:

1. Create a container
2. Run the container
3. Pause the container(optional)
4. Un-pause the container(optional)
5. Start the container
6. Stop the container
7. Restart the container
8. Kill the container
9. Destroy the container

#### Security questions?
###### What is the difference between authentication and authorization?
Authentication means confirming your own identity, while authorization means granting access to the system. In simple terms, authentication is the process of verifying who you are, while authorization is the process of verifying what you have access to.

###### OWASP TOP 10
//TODO: nhớ điền vào

#### LINUX questions?
###### Describe the general file system hierarchy of a Linux system.
- / - root folder
- /etc - configuration files provided by the package manager
- /bin - binaries files
- /sbin - system binaries files (important binaries for the OS)
- /boot - Static files for boot processes ( boot loader)
- /dev - Device files
- /lib - Essential shared libraries and kernel modules
- /usr - Secundary hierarchy
- /mnt - Mounting point for temporary filesystem
- /media - Mounting point for removable media
- /opt - Add-on application software packages
- /srv - Data service provided by this system
- /tmp - Temporary files
- /var - Variable data
- /root - Root user folder
- /home - Home users folders

###### Describe how 'ps' works.
On Linux, the ps command works by reading files in the proc filesystem The directory `/proc/*PID*` contains various files that provide information about process `PID`. The content of these files is generated on the fly by the kernel when a process reads them.

###### Which Linux file types do you know?
Linux file types and ls command identifiers:

- `-` : regular file.
- d : directory.
- c : character device file.
- b : block device file.
- s : local socket file.
- p : named pipe.
- l : symbolic link.

###### Where is password file located in Linux and how can you improve the security of password file?
To improve the security of the password file, instead of using a compatible format we can use shadow password format. So, in shadow password format, the password will be stored as single “x” character which is not the same file (/etc/passwd). This information is stored in another file instead with a file name /etc/shadow. So, to enhance the security, the file is made word readable and also, this file is readable only by the root user. Thus security risks are overcome to a great extent by using the shadow password format.