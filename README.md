## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Topology](https://github.com/peterfboyle25/Azure-Virtual-Network-Project/blob/master/Images/Azure-Virtual-Network.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - [Playbook](https://github.com/peterfboyle25/Azure-Virtual-Network-Project/blob/master/Playbook/docker-elk-beats-playbook.yml)

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
- Load balancers protect the availability of data by providing levels of redundancy in case a server fails or needs to be taken down for maintenance. A jumpbox allows system administrators to configure multiple machines within a security group, from a single machine outside that group, eliminating the need for public access to those devices, and reducing opportunities for malicious activity.

Integrating an ELK server allows users to easily monitor the vulnerable VMs.
- Filebeat monitors and collects log files from specified locations and sends them to the ELK stack.
- Metricbeat collects operating system metrics to send to ELK.

The configuration details of each machine may be found below.

| Name                 | Function    | IP Address | Operating System |
|----------------------|-------------|------------|------------------|
| Jump-Box-Provisioner | Jump Box    | 10.0.0.4   | Linux            |
| DVWA-VM1             | Web Server  | 10.0.0.5   | Linux            |
| DVWA-VM2             | Web Server  | 10.0.0.7   | Linux            |
| DVWA-VM3             | Web Server  | 10.0.0.11  | Linux            |
| DVWA-VM4             | Web Server  | 10.0.0.12  | Linux            |
| ELK-VM               | Data Logger | 10.0.0.8   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 136.49.89.43

Machines within the network can only be accessed by Jump-Box-Provisioner.
- Only my home computer, 136.49.89.43, can access the ELK VM.

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jump-Box-Provisioner | Yes                 | 136.49.89.43         |
| DVWA-VM1             | No                  | 10.0.0.4             |
| DVWA-VM2             | No                  | 10.0.0.4             |
| DVWA-VM3             | No                  | 10.0.0.4             |
| DVWA-VM4             | No                  | 10.0.0.4             |
| ELK-VM               | Yes                 | 136.49.89.43         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible provides a means of creating a standard configuration with a playbook that can be deployed to any number of machines with a single command, eliminating the need to directly access each machine and configure them one at a time.

The playbook implements the following tasks:
- Install docker.io
- Install python-pip
- Install Docker Python module
- Increase virtual memory
- Download and launch ELK container image

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker](https://github.com/peterfboyle25/Azure-Virtual-Network-Project/blob/master/Images/docker-ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.7
- 10.0.0.11
- 10.0.0.12

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors and collects log files from specified locations and sends them to the ELK stack, while Metricbeat gathers metrics from the operating system to send to ELK.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the config file to the Ansible container.
- Update the Ansible/hosts file to include the IPs of hosts that you want to be configured. Each IP should be assigned to a specific host group, either "elkservers" for the ELK machine, or "webservers" for the DVWA machines on which to install Filebeat and Metricbeat. 
- Run the playbook and navigate to the ELK-VM's public IP, port 5601, to check that the installation worked as expected, and the ELK stack is receiving data from Filebeat and Metricbeat.
