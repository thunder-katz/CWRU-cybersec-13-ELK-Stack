## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Topology](https://github.com/thunder-katz/CWRU-cybersec-13-ELK-Stack/blob/main/Diagrams/Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. 
Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml
  - filebeat-config.yml
  - filebeat-playbook.yml
  - metricbeat-config.yml
  - metricbeat-playbook.yml

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
- Load balancers protect the network from being overwhelmed, such as by DDOS attacks.  
- Connecting to the network via a jump box ensures that attack surface is minimized to a single node, while still providing access to a user.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system statistics.
- Filebeat watches for changes to files and records any such instances.
- Metricbeat collects metrics from systems and services, such as CPU usage or Apache.  

The configuration details of each machine may be found below.

| Name          | Function       | IP Address(es)           | Operating System |
|---------------|----------------|--------------------------|------------------|
| Jump Box      | Gateway        | 52.170.147.79 / 10.0.0.4 | Linux            |
| Load Balancer | Direct Traffic | 52.226.81.34             | Linux            |
| Web-3 VM      | Server         | 10.0.0.7                 | Linux            |
| Web-4 VM      | Server         | 10.0.0.8                 | Linux            |
| ELK           | Server         | 10.1.0.4                 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 94.140.9.149

Machines within the network can only be accessed by SSH from the jump box, which has the following IP address:
- 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible? | Allowed IP Addresses |
|----------|----------------------|----------------------|
| Jump Box | Yes                  | 94.140.9.149         |
| Web-3    | No                   | 10.0.0.4             |
| Web-4    | No                   | 10.0.0.4             |
| ELK      | No                   | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The process can be replicated perfectly as many times as required.

The playbook implements the following tasks:
- Install Docker
- Install python3-pip
- Install Docker python module
- Increase virtual memory allocation
- Download and launch a Docker ELK container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

CWRU-cybersec/Images/docker_ps.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- web-3, 10.0.0.7
- web-4, 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors log files for changes, such as the /etc/shadow file.  Metricbeat records operational statistics of the machine and services running on it, such as CPU usage.  

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible.
	- `cp /location/of/install-elk.yml /etc/ansible/install-elk.yml`
- Update the hosts file to include the webservers and ELK server.
	- `nano /etc/ansible/install-elk.yml`
	- Input the machine(s), its IP address(es), and add `ansible_python_interpreter=/usr/bin/python3` to the `hosts` file to set the interpreter
- Copy the playbook(s) for any required beats.
	- `cp /location/of/a_playbook /etc/ansible/a_playbook`
- Run the install-elk.yml playbook, and navigate to http://[your.VM.IP]:5601/app/kibana to check that the installation worked as expected.
	- `ansible-playbook install-elk.yml`
