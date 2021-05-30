# Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ELK-Diagram](https://github.com/egaston24/PROJECT-ELK/blob/main/Diagrams/ELK-Diagram.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook file may be used to install only certain pieces of it, such as Filebeat.

 -[Ansible Playbook](https://github.com/egaston24/PROJECT-ELK/blob/main/Ansible1/my-playbook.yml.txt)
 
 -[Filebeat Playbook](https://github.com/egaston24/PROJECT-ELK/blob/main/Ansible1/Filebeat-playbook.yml.txt)
 
 -[Metricbeat Playbook](https://github.com/egaston24/PROJECT-ELK/blob/main/Ansible1/metricbeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. Load Balancing protects the system from DDoS attacks by shifting attack traffic. If a single server goes down, the load balancer redirects traffic to the remaining online servers. The advantage of a jump box is that it provides a controlled means of access between two dissimilar security zones. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs. Filebeat watches for log files and gathers information. Metricbeat records metrics and statistical data from the operating system and from services running on the server. 

The configuration details of each machine may be found below.

| Name          | Function  | IP Address | Operating System |
|---------------|-----------|------------|------------------|
| Jump Box      | Gateway   | 10.0.0.1   | Linux            |
| Web 1         | Webserver | 10.0.0.7   | Linux            |
| Web 2         | Webserver | 10.0.0.8   | Linux            |
| Web 3         | Webserver | 10.0.0.9   | Linux            |
| ELK-Django VM | Monitoring| 10.1.0.4   | Linux            |
 

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK-Django Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Local Workstation Public IP through TCP 5601

Machines within the network can only be accessed by SSH. The ELK-Server is only accessible from within the ansible container in the Jump Box, IP Address 10.0.0.4, by the SSH key.

A summary of the access policies in place can be found in the table below.

| Name              | Publicly Accessible | Allowed IP Addresses |
|-------------------|---------------------|----------------------|
| Jump Box          | No                  | Local IP on SSH 22   |
| Web 1             | No                  | 10.0.0.7             |        
| Web 2             | No                  | 10.0.0.8             |
| Web 3             | No                  | 10.0.0.9             |
| ELK-Django Server | No                  | Local IP on TCP 5601 |
| Load Balancer     | No                  | Local IP on HTTP 80  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because Ansible lets you quickly and easily deploy multitier apps. You won't need to write custom code to automate your systems; you list the tasks required to be done by writing a playbook, and Ansible will figure out how to get your systems to the state you want them to be in.

The playbook implements the following tasks:
- Configure ELK VM with Docker
- Install Docker.io and Python3-pip
- Increase Virtual memory
- Download and Configure elk docker container
- Set Published Ports

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![DOCKER_PS.PNG](https://github.com/egaston24/PROJECT-ELK/blob/main/Images/DOCKER_PS.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- Web-1 10.0.0.7

- Web-2 10.0.0.8

- Web-3 10.0.0.9

We have installed the following Beats on these machines:

- Filebeat

- Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat watches for log files/locations and collects log events

- Metricbeat records metrics and statistical data from the operating system and from services running on the server

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

 - Copy the filebeat-config.yml and metricbeat-config.yml file to /etc/ansible/files

 - Update the configuration files to include the Private IP of the ELK-Server to the ElasticSearch and Kibana Sections of the Configuration File

 - Run the playbook

 - Navigate to http://[your ELK-VM.External.IP]:5601/app/kibana to check that the installation worked as expected.

The playbook files are:

  - [ELK Installation.txt](https://github.com/egaston24/PROJECT-ELK/blob/main/Ansible1/ELK-Installation.txt) used to install ELK Server
  
  - [Filebeat Playbook](https://github.com/egaston24/PROJECT-ELK/blob/main/Ansible1/Filebeat-playbook.yml.txt)
  
  - [Metricbeat Playbook](https://github.com/egaston24/PROJECT-ELK/blob/main/Ansible1/metricbeat-playbook.yml)

Copy the playbook to: /etc/ansible/

To specify which machine to install the ELK server on versus which to install Filebeat is done by adding the private IP under ELK not webservers.

- update /etc/ansible/hosts

Navigate to http://[your ELK-VM.External.IP]:5601/app/kibana to check thata the ELK Server is running

### Additonal Commands Used

- ssh Redadmin@JumpBox(PrivateIP)

- sudo docker container list -a - Locate the ansible container

- sudo docker start frosty_duck

- sudo docker attach frosty_duck

- cd /etc/ansible

- ansible-playbook elk-playbook.yml (Installs and Configures ELK-Server)

- cd /etc/ansible/

- ansible-playbook beats-playbook.yml (Installs and Configures Beats)

- Open a new browser on Personal Workstation, navigate to (http://[yourELK-Vm.External IP:5601/app/kibana) - This will bring up Kibana Web Portal

