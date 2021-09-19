# CyberBootCampP1
This repository containers all content related to the completion of Project 1

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
 
CyberBootCampP1/Diagrams/Project\ 1\ Diagram\ \(Nicole\ Moore\).pdf

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

  - CyberBootCampP1/Ansible

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
What aspect of security do load balancers protect? What is the advantage of a jump box? Load balancers help to protect against denial-of-service attacks because it shifts the attacking traffic across various points to ensure that the system is not overwhelmed and can remain available. The advantage of a jimp box is that it allows users access from a single-entry point that can be easily secured and monitored. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system metrics.
What does Filebeat watch for? Filebeat monitors for changes made to any information in the file system and when those changes happen. 
What does Metricbeat record? Metricbeat collects metrics and statistics to the system and sends the information to the location that you specify. 

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.5   | Linux            |
| Web-1    | Server   | 10.0.0.6   | Linux            |
| Wrb-2    | Server   | 10.0.0.7   | Linux            |
| Elk-VM   | Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-Whitelisted IP addresses: 207.181.255.147

Machines within the network can only be accessed by the Jump Box.
Which machine did you allow to access your ELK VM? What was its IP address? The Jump Box Public IP: 13.89.49.50 Private IP: 10.0.0.5

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses|
|----------|---------------------|---------------------|
| Jump Box | Yes                 | 207.181.255.147     |
| Web-1    | No                  | 10.0.0.5            |
| Wrb-2    | No                  | 10.0.0.5            |
| Elk-VM   | No                  | 10.1.0.5            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? The advantage of automating configuration with Ansible is that you can run commands and install services on multiple servers from a single playbook. 

The playbook implements the following tasks:
-	Installs docker.io
-	Installs python3-pip
-	Installs docker
-	Runs command sysctl -w vm.max_map_count=262144
-	Use more memory vm.max_map_count
-	Launch docker container elk
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

 

CyberBootCampP1/Ansible/ Docker\ ps\ output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-	Web-1 10.0.0.6
-	Web-2 10.0.0.7

We have installed the following Beats on these machines:
-	Filebeat
-	Metricbeat

These Beats allow us to collect the following information from each machine:
-In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc.
Filebeat collects information on changes made to the file system. Metricbeat collects information on the metrics and statistics of the system. 
 

 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml
 file to the web vms.
- Update the filebeat-config.yml file to include
-	The IP address of your Elk VM on line 1106 and 1806
-	Edit the host file- uncomment [webservers] add your Web vms and their Ips and ansible_python_interpreter=/usr/bin/python3
-	
- Run the playbook, and navigate to the web vms to check that the installation worked as expected.

_Answer the following questions to fill in the blanks: 
- _Which file is the playbook? Where do you copy it? /etc/ansible/file/filebeat-configuration.yml

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? The host file. Edit the /etc/ansible/host file to add webserver/elkserver ip addresses and ansible_python_interpreter=/usr/bin/python3

- _Which URL do you navigate to in order to check that the ELK server is running? http://13.90.90.142:5601/app/kibana#/home 13.90.90.142 is the Public IP for the load balancer and 5601 is the port it is accessible from.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

