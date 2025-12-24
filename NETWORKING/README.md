# Networking

## Essential Networking Concepts with examples

Think we are making a website.

How user can access our website from their browser?
- IP Address
    - Public IP address
    HTTP **request** 
    HTTP **response**

Now IP address is in numbers, its hard to remember.
- HERE comes DNS (Domain Name System)
    - Domain Name
    - DNS translates domain names to IP addresses so browsers can load Internet resources.

Now our website is sharing three different things - WebApp, Database, Backend Logic on the same IP address. How request know which application to go to?
- PORTS: 
    - Each application is assigned a port number.
    - Example: HTTP uses port 80, HTTPS uses port 443, MySQL uses port 3306 etc.

Hosting everything on a single ip address, what if hacker wants to attack our website?
- Subnets
    - A subnet, or subnetwork, is a segmented piece of a larger network. 
    - Subnets are designed to divide large networks into smaller, more efficient subnetworks.
    - Example: Our website's web server is on one subnet, and the database server is on another subnet. This way, if one subnet is compromised, the other remains secure. 

Now how do subnets communicate with each other?
- Routers
    - How to get from one subnet to another subnet?
    - A router is a networking device that forwards data packets between computer networks.

We can't open all ports to the public, how do we secure our application?
- Firewalls
    - We declare policy and rules to allow or block traffic.
    - Example: Only allow traffic on port 80 and 443 to the web server, block all other ports.

Now we need to scale our application to handle more users. We now had 50 backend servers in backend for security. These have private IP addresses. How do we route traffic to these servers?
- Its like we can communitcate between private IP but not with Public IP. We also can't give each a public IP.
- Here comes NAT (Network Address Translation)
    - NAT is a method of remapping one IP address space into another by modifying network address information in the IP header of packets while they are in transit across a traffic routing device.
    - Example: A NAT device can take requests from the public internet and forward them to the appropriate private IP addresses in the backend.
    - This way,hidden and protected, Single Public IP ~ no less cost than alotting Public IP to each server

Now we are handling hardware, so we decided to move to cloud.
- VPC (Virtual Private Cloud)
    - A VPC is a virtual network dedicated to your AWS account. It is logically isolated from other virtual networks in the AWS Cloud.
    - Example: In AWS, you can create a VPC for your web application, where you can define subnets, route tables, and security settings to control the flow of traffic within your application.
    - We still have Public and Private subnets in VPC.
    We need Internet Gateway to connect Public subnet to Internet.
    - We have route table which tell us where to go.
    - Each subnet has route table which route traffic.
    - We place a NAT Gateway in Public subnet to allow Private subnet to access Internet.

As we grow, it is more complex to manage everything manually. We now have more dependencies, more services, more things to configure, we need to go microservices to make it scalable.
- Containers comes into picture.
    - A container packages an application and its dependencies together. Multiple containers can run on the same machine and share the OS kernel with other containers, each running as isolated processes in user space.
    - It is easy to move containers between environments.
    - We use Docker to containerize all of our services. i.e Laptop, Server, Cloud.

Now container introduce new networking challenges.
- Container Networking
    When we run containers they need to communicate with each other. Docker makes a bridge network by default.
    - Bridge Network: A bridge network is a private internal network created by Docker on the host machine. Containers on the same bridge network can communicate with each other using their IP addresses or container names.
    
    Containers have their own networking inside them. Like they can use port 9000 to communicate to other service

    So how do external request reach to container?
    - When request comes for eg to port 9000 it need to go to that service. so we maps port 9000 of host to port 9000 of container.
    - It is similar to NAT concept.

Now we have multiple containers running on multiple servers. How do we manage networking between them?
- Overlay Networks
    Overlay Network create a Virtual Network that spans across multiple Docker hosts. It allows containers running on different hosts to communicate with each other as if they were on the same local network.

Now we have to manage hundred of containers. Managing networking manually is not possible.
- Which server should a new container go to?
- What happens if a server goes down?
- How do container find each other when they are dynamic (i.e Keep moving from one server to another)?

We use automate all of this using Container Orchestration tools like Kubernetes.
- Kubernetes basic unit is a POD. It is group of one or more containers.
- Each POD gets its own IP address.
- Kubernetes has built-in networking model to manage communication between PODs, Services, and external world.
- Pods are temporary, it can move, delete and when we create it gets a new IP address. When new POD is created how other POD find it?
    - Here comes **Service Discovery**.
    - It has DNS built-in to find PODs using their names.
    - eg backend-service -> gives IP of PODs running backend.
    - If backend pod dies, new POD is created with new IP, DNS is updated automatically.

Now we need to expose our application to the internet.
- We use **Ingress** Controller.
    So single ingress can handle all incoming traffic and route to appropriate services based on rules that we configure.
    