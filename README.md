## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

- ChrisMee1/Elk_Project/Diagram/Cloud Diagram.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

- The ansible-playbooks and the filebeat-playbook are needed to create and implment the Elk-Sever. 
   - ChisMee1/Elk_Project/Ansible you will find the playbooks.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
The load balancer ensures that work to process incoming traffic will be shared by both vulnerable web servers. Access controls will ensure that only authorized users — namely, ourselves — will be able to connect in the first place.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system of the VMs on the network and system metrics.
- Filebeat monitors the log files or locations that you specify.
- Metricbeat records the metrics and statics from the operation system running from the server.

The configuration details of each machine may be found below.

| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.4   | Linux            |
| Web-1    | Webserver 1| 10.0.0.5   | Linux            |
| Web-2    | Webserver 2| 10.0.0.6   | Linux            |
| ElK      | Webserver  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP Address
       
Machines within the network can only be accessed by Jump box virtual machine
- The Jump box VM has access to the ELK VM. The IP address of the Jump box is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses   |
|----------|---------------------|------------------------|
| Jump Box | No                  | Personal IP/10.0.0.4|
|   Web-1  | No                  | 10.0.0.5               |
|   Web-2  | No                  | 10.0.0.6               |
|   ELK    | No                  | 10.1.0.4               |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible allows IT administers to automate their daily tasks and save a lot of time. That frees them to focus on more important business.
 
The playbook implements the following tasks:
- Install Docker
- Install python3-pip
- Set the vm.max_map_count to 26144
- Download and launch docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

ChrisMee1/Elk_project/Images/Elk_docker_ps.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1, 10.0.0.5
- Web-2, 10.0.0.6
We have installed the following Beats on these machines:
- Filebeat
- Metricbeat
These Beats allow us to collect the following information from each machine:
- Filebeat, monitors the logfiles and locations that you specify, which we use to see changes in the log files. Example, you would be able to see a kill command happened
- Metricbeat, records the metrics and statistics from the operation system and from the sever. We could use it to look how much RAM or CPU usage was being used on the webserver at a certain time.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible.cfg file to /etc/ansible.
- Update the  file to include...
- Run the playbook, and navigate to Ansible Container and SSH into your elk server to check that the installation worked as expected.

Which file is the playbook?
- Ansible-config.yml
 Where do you copy it?
- In your Docker container.
Which file do you update to make Ansible run the playbook on a specific machine? 
- You run anisble-playbook on the Docker Container VM
How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- Install Elk on the Jump Box, and install Filebeat on the Docker Container VM
Which URL do you navigate to in order to check that the ELK server is running?
- http://public IP:5601/app/kibana

The commands needed to run the Ansible configuration for the Elk-Server are:
* ssh azureuser@ 20.83.187.166 (JumpBox)
* sudo docker container list -a (locate your ansible container)
* sudo docker start container (name of the container)
* sudo docker attach container (name of the container)
* cd /etc/ansible/
* ansible-playbook elk.yml (configures Elk-Server and starts the Elk container on the Elk-Server) wait a couple minutes for the implementation of the Elk-Server
* cd /etc/ansible/roles/
* ansible-playbook filebeat-playbook.yml (installs Filebeat and Metricbeat)
* open a new web browser (Elk-Server PublicIP:5601) This will bring up the Kibana Web Portal

