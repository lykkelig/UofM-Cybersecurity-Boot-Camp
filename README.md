# UofM-Cybersecurity-Boot-Camp
Ron Hankey - University of Minnesota Cybersecurity Boot Camp
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

  

Network Diagram: (https://github.com/lykkelig/UofM-Cybersecurity-Boot-Camp/blob/main/Diagrams/Ron%20Hankey%20-%20Unit%2013%20Homework.pdf)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the *.yml file may be used to install only certain pieces of it, such as Filebeat.

 Enter the playbook file._
  https://github.com/lykkelig/UofM-Cybersecurity-Boot-Camp/blob/main/Ansible/pentest.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting outside traffic to the network.
What aspect of security do load balancers protect? What is the advantage of a jump box?_
A load balancer should add protection for a DDoS type of attack. Load balancers balance the traffic betwen servers so no one server is overloaded. A jump box adds the advantage of being a single point of entry to the VM's for maintenance. The servers themselves are not exposed to a direct connection, that is only done through the jump box which should be highly secured.  

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the server and system logs.
What does Filebeat watch for?_
Filebeat is a log shipper that is installed as an agent on your server(s). Filebeat will monitor the log files or locations that you specify, catalogs log events, and sends them to Elasticsearch or a log stash for indexing.

What does Metricbeat record?
Metricbeat will collect metrics from systems and the services running. Examples include monitoring CPU utilization to memory use and disk storage. Metricbeat is a metric shipper used for monitoring systems and the processes running on them.

The configuration details of each machine may be found below.

| Name     | Function | IP Address              | Operating System |
|----------|----------|-------------------------|------------------|
| Jump Box | Gateway  | 10.0.0.4/40.83.12.148   | Ubuntu Linux     |
| Web-1    | Web Srvr | 10.0.0.5/40.122.185.183 | Ubuntu Linux     |
| Web-2    | Web Srvr | 10.0.0.6/40.122.185.183 | Ubuntu Linux     |
| ELK Srvr | Monitor  | 10.1.0.4/157.55.171.181 | Ubuntu Linux     |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Add whitelisted IP addresses_
My home IP address: 199.48.94.126

Machines within the network can only be accessed by connecting to the jump box.
Which machine did you allow to access your ELK VM? What was its IP address?_
My home PC 199.48.94.126 and the jump box 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 199.48.94.126        |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| ELK Srvr | Yes                 | 199.48.94.126        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?_
You can create a yml file to perform the configuration which can be scaled to perform maintenance on 1000's of machines.
This is much quicker and more efficient than having a person perform these tasks manually.

The playbook implements the following tasks:
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- 1) Configure the ELK server with Docker
- 2) Install the Docker container
- 3) Install Python
- 4) Increase system memory
- 5) Download and install the ELK container
- 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

**Note**: The following image link needs to be updated. Replace `docker_ps_output.png` with the name of your screenshot image file.  


The path with the name of your screenshot of docker ps output (https://github.com/lykkelig/UofM-Cybersecurity-Boot-Camp/commit/9cc51009c1577c9b65e84ac0d5b8d9c9d981ba13)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring_
10.0.0.5
10.0.0.6

We have installed the following Beats on these machines:
Specify which Beats you successfully installed_
filebeat-7.6.1-amd64.deb

These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
The slowlog allows the capture of query and fetch phases into a dedicated log.
Server log files capture raw and unfiltered traffic on the hosted website. Every time any browser or user-agent (example: Google), makes a resource request for a pages or images or javascript file or any other content from your web server, the server inserts a line into the log file.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to the roles directory.
- Update the hosts file to include the IP addresses of the target systems.
- Run the playbook, and navigate to http://157.55.171.181:5601/app/kibana to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- _Which file is the playbook? filebeat-config.yml (https://github.com/lykkelig/UofM-Cybersecurity-Boot-Camp/blob/main/Ansible/filebeat-config.yml)
  Where do you copy it?_ The directory: /etc/ansible/roles/
- _Which file do you update to make Ansible run the playbook on a specific machine? hosts
(https://github.com/lykkelig/UofM-Cybersecurity-Boot-Camp/blob/main/Ansible/hosts)
 How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
 In the hosts file there is tag which distinguishes between the VM's [webservers] and the ELK server [elk].
- _Which URL do you navigate to in order to check that the ELK server is running?
http://157.55.171.181:5601/app/kibana#/home

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
1) sudo docker cp bold_rosalind:/home/azureuser/ansible/  .

2) scp -r azureuser@40.83.12.148:/home/azureuser/ .
