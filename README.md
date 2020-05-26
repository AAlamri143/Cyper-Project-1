## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/VM.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the install-elk.yml file may be used to install only certain pieces of it, such as Filebeat.



This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly valable becuae it is redundant, in addition to restricting access to the network.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system performance metrics.


|   Name   | Function | IP Address |  Operating System  |
|----------|----------|------------|--------------------|
| Jump Box | Gateway  |  10.0.1.4  | Linux ubuntu 18.04 |
| DVWA-VM1 | Web app  |  10.0.1.5  | Linux ubuntu 18.04 |
| DVWA-VM2 | Web app  |  10.0.1.6  | Linux ubuntu 18.04 |
| DVWA-VM3 | Web app  |  10.0.1.9  | Linux ubuntu 18.04 |
| DVWA-VM4 | Web app  | 10.0.1.10  | Linux ubuntu 18.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the load balancer & the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
* 51.141.175.21
* 20.42.147.230

Machines within the network can only be accessed by ort (22) jumpbox server 10.0.1.4

A summary of the access policies in place can be found in the table below.

|      Name      | Publicly Accessible |  Allowed IP Addresses  |
|----------------|---------------------|------------------------|
|    Jump Box    |         Yes         |     51.141.175.21      |
| Load balancer  |         Yes         |     20.42.147.230      |
|    Elk stack   |         No          |  all VW1,2,3,4 jumpbox |
|        ~       |          ~          |        10.0.1.4        |
|        ~       |          ~          |        10.0.1.5        |
|        ~       |          ~          |        10.0.1.6        |
|        ~       |          ~          |        10.0.1.9        |
|        ~       |          ~          |        10.0.1.10       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because ansible is allowing for IAC Infrastructure as Code‎.

The playbook implements the following tasks:
* Change the memory on the host machine
* Installing docker.io
* Installing python-pip
* Installing Docker python module
* downloading and launch a docker elk stack


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(Images/dockerPS.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
* 10.0.1.5
* 10.0.1.6
* 10.0.1.9
* 10.0.1.10

We have installed the following Beats on these machines:
Filebeat-7.7.0-derwin-x86_64.tar.gz

These Beats allow us to collect the following information from each machine:
Filebeat: collects Widnows logs which we use to track user logon event, and so in Kibana. `

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Filebeat Configuration file to the DVWA-VMs.
- Update the hosts file to include:
#### [webservers]
* 10.0.1.5
* 10.0.1.6
* 10.0.1.9
* 10.0.1.10
#### [elkservers]
* 10.0.1.4

- Run the playbook, and navigate to Kibana to check that the installation worked as expected.


**Bonus**
The specific command the user will need to run to download the playbook, update the files, etc. is:
$ ansible-playbook filebeat-playbook.yml 