
# 0x0A. Web infrastructure design #0

### Author: Lawal Afeez 
## Synopsis
This project applies newly learned concepts about web infrastructure.

### At the end of this project students should be able to explain to anyone, **without the help of Google**:
*   You must be able to draw a diagram covering the web stack you built with the sysadmin/devops track projects
*   You must be able to explain what are each component doing
*   You must be able to explain system redundancy
*   Know all the mentioned acronyms: LAMP, SPOF, QPS



### Project Requirements
*   A `README.md` file, at the root of the folder of the project, is mandatory
*   For each task, once you are done whiteboarding (on a whiteboard, piece of paper or software or your choice), take a picture/screenshot of your diagram
*   This project will be manually reviewed:
	*   As each task is completed, the name of that task will turn green
	*   Upload a screenshot, showing that you completed the required levels, to any image hosting service (I personally use [imgur](http://imgur.com/) but feel free to use anything you want).
	*   For the following tasks, insert the link from of your screenshot into the answer file
	*   After pushing your answer file to Github, insert the Github file link into the URL box
*   You will also have to whiteboard each task in front of a mentor, staff or student - no computer or notes will be allowed during the whiteboarding session
	*   Focus on what you are being asked:
	*   Cover what the requirements mention, we will explore details in a later project
	*   Keep in mind that you will have 30 minutes to perform the exercise, you will get points for what is asked in requirements
	*   Similarly in a job interview, you should answer what the interviewer asked for, be careful about being too verbose - always ask the interviewer if going into details is necessary - speaking too much can play against you
	*   In this project, again, avoid going in details if not asked

## Project Breakdown
Task # | Type | Short description | File name and link |
---: | --- | --- | --- |
0 | **Mandatory** |<p>A lot of websites are powered by simple web infrastructure, a lot of time it is composed of a single server with a <a href="https://en.wikipedia.org/wiki/LAMP_(software_bundle)">LAMP stack</a>.</p><p>On a whiteboard, design a one server web infrastructure that hosts the website that is reachable via <code>www.foobar.com</code>. Start your explanation by having a user wanting to access your website.</p><p>Requirements:</p><ul><li> You must use:<ul><li>1 server</li><li>1 web server (Nginx)</li><li>1 application files (your code base)</li><li>1 database (MySQL)</li><li>1 domain name <code>foobar.com</code> configured with a <code>www</code> record that points to your server IP <code>8.8.8.8</code></li></ul></li><li>You must be able to explain some specifics about this infrastructure:<ul><li>What is a server</li><li>What is the role of the domain name</li><li>What type of DNS record <code>www</code> is in <code>www.foobar.com</code></li><li>What is the role of the web server</li><li>What is the role of the database</li><li>What is the server using to communicate with the computer of the user requesting the website</li></ul></li><li>You must be able to explain what are the issues with this infrastructure:<ul><li>SPOF</li><li>Downtime when maintenance needed (like deploying new code web server needs to be restarted)</li><li>Cannot scale if too much incoming traffic</li></ul></li></ul> | [0-simple_web_stack](./0-simple_web_stack)
1 | **Mandatory** |<p>On a whiteboard, design a three servers web infrastructure that host the website <code>www.foobar.com</code>.</p><p>Requirements:</p><ul><li> You must add:<ul><li>2 servers</li><li>1 web server (Nginx)</li><li>1 load-balancer (HAproxy)</li><li>1 application files (your code base)</li><li>1 database (MySQL)</li></ul></li><li>You must be able to explain some specifics about this infrastructure:<ul><li>For every additional element, why you are adding it</li><li>What distribution algorithm your load balancer is configured with and how it works</li><li>Is your load-balancer enabling an Active-Active or Active-Passive setup, explain the difference between both</li><li>How a database Primary-Replica (Master-Slave) cluster works</li><li>What is the difference between the Primary node and the Replica node in regard to the application</li></ul></li><li>You must be able to explain what are the issues with this infrastructure:<ul><li>Where are SPOF</li><li>Security issue (no firewall, no HTTPS)</li><li>No monitoring</li></ul></li></ul> | [1-distributed_web_infrastructure](./1-distributed_web_infrastructure)
2 | **Mandatory** |<p>On a whiteboard, design a three servers web infrastructure that host the website <code>www.foobar.com</code>, it must be secured, serve encrypted traffic and be monitored.</p><p>Requirements:</p><ul><li> You must add:<ul><li>3 firewalls </li><li>1 SSL certificate to serve <code>www.foobar.com</code> over HTTPS</li><li>3 monitoring clients (data collector for Sumologic or other monitoring services)</li></ul></li><li>You must be able to explain some specifics about this infrastructure:<ul><li>For every additional element, why you are adding it</li><li>What are firewalls for</li><li>Why is the traffic served over HTTPS</li><li>What monitoring is used for</li><li>How is the monitoring tool collecting data</li><li>Explain what to do if you want to monitor your web server QPS</li></ul></li><li>You must be able to explain what are the issues with this infrastructure:<ul><li>Why terminating SSL at the load balancer level is an issue</li><li>Why having only one MySQL server capable of accepting writes is an issue</li></ul></li></ul> | [2-secured_and_monitored_web_infrastructure](./2-secured_and_monitored_web_infrastructure)
3 | *Advanced* |  <p>Readme</p>    <ul>  <li><a href="https://www.nginx.com/resources/glossary/application-server-vs-web-server/">Application server vs web server</a></li>  </ul>    <p>Requirements:</p>    <ul>  <li> You must add:    <ul>  <li>1 server</li>  <li>1 load-balancer (HAproxy) configured as cluster with the other one</li>  <li>2 web application servers (Gunicorn)</li>  </ul></li>  <li>You must be able to explain some specifics about this infrastructure:    <ul>  <li>For every additional element, why you are adding it</li>  </ul></li>  </ul> | [3-scale_up](./scale_up)

# What one must be able to explain about task 0
* ### What is a server
<p>Servers are physical machines (as hardwares), virtual machines or softwares (computer programs) that serve or provide functionality to other programs or devices called “clients”. The term server comes from queuing theory used in Kendall’s notation, where servers serve or process the clients requirements in the same way as a telephone operator, a cooker or a production machine process incoming orders, having in mind its capacity and service process time.

A computer can function as a server, and a server can be a computer, both of them being built up with hardware and software. However, the main difference between these two is the capacity and computer power servers have. In other words, servers are computers on steroids with faster processing capacity. They are usually stored in data centers racks (stacks of servers piled one on top of each other).

On the other hand, virtual servers function more like virtual machines, or virtual computers. These are a virtual representation of the physical servers, having their own operating system and applications (Posey, 2021).</p>

* ### What is the role of the domain name
<p>The role of the domain name is to replace complex IP addresses numbers into easily understandable names so humans can remember and communicate them in a better way.</p>

* ### What type of DNS record www is in www.foobar.com
<p> DNS record of www belongs to a subdomain of the www.foobar.com. It is an A record type of DNS</p>

* ### What is the role of the web server
</p> Web servers are what make Web hosting possible, that is, the possibility of renting a space on a server to store the files of our site.</p>

* ### The fundamental role of a Web Server
<p>The main function of a Web server is to store the files of a site and broadcast them over the Internet so that they can be visited by users. Basically, a web server is a large computer that stores and transmits data via the network system called the Internet. When a user enters an Internet page, his browser communicates with the server sending and receiving data that determines what he sees on the screen. Therefore, we say that Web servers are to store and transmit data from a site as requested by a visitor’s browser.</p>

* ### What is the role of the application server
<p>The application server is the intermediary between browser-based databases and back-end databases and legacy systems. In many uses, the application server combines or works with a web server (Hypertext Transfer Protocol) and is called a web application server.

What is the role of the database
The role of the database is to make the information gathered organized so it can be easily accessed, managed and updated. However, not all database management systems work the same, and the mechanisms they use to organize data can vary, ranging from relational database to object-oriented database, distributed database or cloud database.</p>

* ### What is the server using to communicate with the computer of the user requesting the website
<p> The server is using HTTP to communicate with the computer.</p>

* ### Issues with the simple web infrastructure
<p>One of the issues of having a simple web infrastructure, has to do with the SPOF (Single Point of Failure) where if component of the system fails, there is no backup that can support the continuity of the functionality of the system, bringing the whole system to a collapse by being unable to operate.</p>
<p>Also, whenever some structure or node in the system needs to be repaired, the whole system has to be shut down, while the maintenance is done. Then, client requests cannot be attended during this period of time.</p>
<p>Overload of traffic can be a risk to the server capacity. This, because there is no possibility to scale the service with additional servers as backup. Leading to a possible breakdown of the web page and client requests, as traffic surpasess servers capacity.</p>

# What one must be able to explain about task 1

* ### For additional element, why you are adding it?
<p>The new configuration is composed of two master-servers and one slave-servers. As the master-servers are going to be working based on a Active-Active set up, their configuration must be identical, therefore we need to add every additional element as the simple web infrastructure we had in the previous point. The load is going to be managed through a load-balancer, which distributes the queries according to a Robin-Round algorithm. Finally an additional server will be needed to serve a replica or slave server, helping to unload the masters servers reading queries.</p> 

* ### What distribution algorithm your load balancer is configured with and how it works
<p> The load balancer is using Round RObin algorithm.</p>

* ### Is your load-balancer enabling an Active-Active or Active-Passive setup, explain the difference between both
<p> The load balancer is using the two i.e both active-active and active-passive</p>

# What one must be able to explain about task 2

* ### For every additional element, why you are adding it
<p>3 Firewalls: The first Firewall checks the rules after receiving the requests and could deny following requests. The second firewall is working in the server to prevent someone hacking depending of the requests, and the third firewall acts as a circuit-level firewalls, inspect the transaction of the information.</p>
</p>SSL certificate: 1 SSL certificate: is added to secure https protocols and encrypt communication. Then, the ‘plain text’ won’t be easy accessed or viewed by a third person, making the protocol communication and data transfer form the browser and web server more secure (Instant SSL, 2021)</p>

* ### What are firewalls for
<P>Firewalls is a network security device that monitors network traffic, it can be understood as a division or “wall” between a private network and public network which limits and blocks network traffic based on a set of security rules in the hardware or software by analyzing data packets that request entry to the network. Additionally, firewalls are used to allow remote access to a private network through secure authentication (Beal, 1996)</P>

* ### Why is the traffic served over HTTPS
<P>HTTPS stands for HyperText Transfer Protocol Secure, and the traffic is served in order to bring protection by using the secure port 443, which encrypts outgoing information. Then it is more difficult to spy or get access to the site’s information.</P>

* ### What monitoring is used for
<P>Monitoring is practice used for quality control. As Peter Ducker said, “What can’t be measured, it can’t be improved”. Then, monitoring not only helps to make sure to maintain high quality levels, keeping the established standards and consistency, but also to help in the continuous improvement of the resources performance.</P>

* ### How the monitoring tool is collecting data
<p>IT monitoring is composed of three parts: 1) Fundation; 2) Software, and 3) Interpretation in order to function.

Foundation: Are related to the infrastructure at its lowest layer of the software stack. This includes physical and virtual devices, such as servers, CPUs and VMs.
Software: The software is the monitoring section which analyzes what is happening in the devices (physical or virtual machines) in terms of CPU usage, load, memory, and running count.
Interpretation: Here is where collected data is turned into metrics and are presented through graphs or data charts (mostly on GUI dashboard). This is often integrated with tools of data visualization to help better understand and do data analytics of performance (Gillis, 2020).</p>

* ### Explain what to do if you want to monitor your web server QPS
<p>Queries per second is a measure of the rate of traffic going in a particular server serving a Web domain. It is an important metric to monitor, because it can help you decide whether to scale the server in order to cope with the demand of usage, and resource requirement so the web page won’t collapse in the future with overload server request.</p>



