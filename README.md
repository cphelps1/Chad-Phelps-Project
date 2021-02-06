## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!https://drive.google.com/drive/folders/1t-HtA-gdt-7OXHd-q8awUWdmkXfxH_nq?usp=sharing(Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secured, in addition to restricting acces to the network.
- the Load Balance restrict access to port on the network? The advantage of a jump box is has all the controls to the Web VMs and Elk server.  Plus, it have the yml files to load programs to the Elk server and tells the Web VMs how to give access to the Elk server for motioring.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the web VMs and system contrls.
- Filebeat watch for access and change to system.
- Metricbeat record is a collection of metrics from the web VMs operating system and services running on your servers.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.12  | Linux            |
| web-1    |          | 10.1.0.10  | Linux            |
| web-2    |          | 10.1.0.11  | linux            |
| web-3    |          | 10.1.0.13  | linux            |
| ELK-1    |          | 10.0.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox-provisional machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 72.238.111.53

Machines within the network can only be accessed by load balancer.
- Any IP can allow to access your ELK VM? The IP address is 137.117.70.145.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | no                  | 10.1.0.12            |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- By using a yml playbook to setup the elk machine it did all the setup commands at once and you can see right away if there was an error.  

The playbook implements the following tasks:

- the first steps installed docker and python3-pip
- the next step increased memory to 262144
- the next step set the containers and ports
- the next step restarted docker
- the next step enable the service on boot


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![https://drive.google.com/drive/folders/1t-HtA-gdt-7OXHd-q8awUWdmkXfxH_nq?usp=sharing](Images/chad phelps kibana screenshot.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.1.0.10, 10.1.0.11, 10.1.0.13

We have installed the following Beats on these machines:
- filebeats-playbook, microbeats-playbook

These Beats allow us to collect the following information from each machine:
- filebeats collect all systems logs, sudo commands, ssh logins and new names and user groups.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeats-playbook.yml file to ansible folder.
- Update the hosts file to include by adding to elk after webservers 10.0.0.4 ansible_python_interpreter=/usr/bin/python3
- Run the playbook, and navigate to elk server http://137.117.70.145:5601/app/kibana#/home to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? filebook-playbook.doc and it is saved google drive project 1/playbooks.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?  hosts: elk not on hosts: webservers
- _Which URL do you navigate to in order to check that the ELK server is running? 137.117.70.145:5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
to run the playbooks:
first login to ansible by using sudo docker start -ai loving_turing.  this is where my containers are located. change your dir to etc/ansible
ansible-playbook install-elk.yml
ansible-playbook filebeats-playbook.yml
ansible-playbook metricbeat-playbook.yml


