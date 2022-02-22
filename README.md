## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![NetDiagram](https://i.imgur.com/3Xa0KDC.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

  - [elk installation](https://github.com/CartHackByte/Elk_Stack/blob/main/ansible/install-elk.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient in addition to restricting traffic to the network.
- What aspect of security do load balancers protect? 
    - Load balancers protects the system from DDoS attacks by shifting attack traffic.
    - Load Balancing contributes to the Availability aspect of security in regards to the CIA Triad.

- What is the advantage of a jump box?
 - The advantage of a jump box is to give access to the user from a single node that can be secured and monitored.
 - The advantage of a JumpBox is the orgination point for launching Administrative Tasks. This ultimately sets the JumpBox as a SAW (Secure Admin Workstation). All Administrators when conducting any Administrative Task will be required to connect to the JumpBox (SAW) before perfoming any task/assignment.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Logs and system traffic.
- Filebeat watches for any information in the file system which has been changed and when it has.
- Filebeat watches for log files/locations and collects log events
- Metricbeat takes the metrics and statistics that collects and ships them to the output you specify.
- Metricbeat records metric and statistical data from the operating system and from services running on the server.

The configuration details of each machine may be found below.


| Name       | Function  | IP Address | Operating System   |
|------------|-----------|------------|--------------------|
| Jump Box   | Gateway   | 10.0.0.4   | Linux Ubuntu 18.04 |
| Web 1      | Server    | 10.0.0.6   | Linux Ubuntu 18.04 |
| Web 2      | Server    | 10.0.0.7   | Linux Ubuntu 18.04 |
| ElkStackVM | ELKserver | 10.3.0.4   | Linux Ubuntu 18.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 137.134.115.12

Machines within the network can only be accessed by SSH.
- The Jump Box, private IP on the vnet is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Address |
|------------|---------------------|--------------------|
| Jump Box   | No                  | 10.0.0.4           |
| Web 1      | No                  | 10.0.0.6           |
| Web 2      | No                  | 10.0.0.7           |
| ElkStackVM | No                  | 10.3.0.4           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- This allows you to deploy to multiple servers using a single playbook

The playbook implements the following tasks:
- Install docker.io
- Install Python-pip
- Install docker container
- Launch docker container: elk
- Command: sysctl -w vm.max_map_count=262144

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![DockerPS](https://i.imgur.com/8NwlVVs.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 and Web-2, 10.0.0.6, 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat - Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors log files or locations you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat collects metrics from the operating system and from services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to etc/ansible
- Update the configuration file to include webservers and ELKvm private IPs
- Run the playbook, and navigate to Elkvm to check that the installation worked as expected.

![KibanaDash](https://i.imgur.com/ojirTMZ.png)

Answer the following questions to fill in the blanks:_
- Which file is the playbook? Where do you copy it? /etc/ansible/file/filebeat-configuration.yml
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ edit the /etc/ansible/hosts file to add webserver/elkserver ip addresses
- Which URL do you navigate to in order to check that the ELK server is running? http://[your.ELK-VM.External.IP]:5601/app/kibana


