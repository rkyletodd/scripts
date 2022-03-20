## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


![RedTeam ELK Network Diagram](https://github.com/rkyletodd/scripts-Project-1/blob/308e1f2df4e72f7b5b3e98eb3cab2ca366d08c07/diagrams-images/Project%201%20RedTeam%20Elk%20VM%20Network%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - [Ansible Pentest Playbook File](https://github.com/rkyletodd/scripts-Project-1/blob/main/ansible-linux/ansible-pentest.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available and redundant, in addition to restricting access to the network.
- Load balancers distribute traffic between the network servers, ensuring a balance and that no one server is being overwhelmed with requests.
- The purpose of the Jump Box Provisioner is to be as a gateway and location of the Ansible container. Jumpbox is where Ansible playbooks are deployed; specifically installing the DVWA containers, metricbeat, and filebeat on each DVWA VM, as well as the ELK Stack container on the ELK-Server VM.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.

- Filebeat monitors log files, collects log events, and then passes them on to elasticsearch for indexing purposes.
- Metricbeat collects data and metrics from the system and services running on one's server, and sends them to elasticsearch.
The configuration details of each machine may be found below.

|    Name    |       Function      | IP Address | Operating System |   |
|:----------:|:-------------------:|:----------:|:----------------:|:-:|
| JumpBox VM |       Gateway       |  10.0.0.5  |       Linux      |   |
| ELK Server | ELK Stack Container |  10.1.0.4  |       Linux      |   |
|   Web1 VM  |         DVWA        |  10.0.0.6  |       Linux      |   |
|   Web2 VM  |         DVWA        |  10.0.0.7  |       Linux      |   |
|  Web3 VM   |         DVWA        |  10.0.0.9  |       Linux      |   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.201.121.83 (Workstation)

Machines within the network can only be accessed by JumpBox.
- The Elk-VM (10.1.0.4) is accessible using SSH from the JumpBox VM, and also from the user's workstation in order to access the Kibana application via Port 5601.
- The DWVA machines are accessible using HTTP from the workstation, but only through the load balancer (20.127.90.70).

A summary of the access policies in place can be found in the table below.

|    Name    | Publicly Accessible? |                    Allowed IP Addresses                    |
|:----------:|:--------------------:|:----------------------------------------------------------:|
| JumpBox VM |          Yes         |                        73.201.121.83                       |
| ELK Server |          Yes         | 73.201.121.83, 10.0.0.5, 10.0.0.6, <br> 10.0.0.7, 10.0.0.9 |
|   Web1 VM  |          No          |                   20.127.90.70, 10.0.0.5                   |
|   Web2 VM  |          No          |                   20.127.90.70, 10.0.0.5                   |
|  Web3 VM   |          No          |                   20.127.90.70, 10.0.0.5                   |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because automating the configuration allows more flexibility for future updates, enables easy reproduction for future similar tasks, and reduces the likelihood of future mistakes in the configurations.

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install docker module
- Increase the amount of virtual memory and uses that additional memory, by setting the vm.max_map_count to 262144.
- Download and launch the docker elk container
- Use systemd to enable docker service on boot, so that docker does not require restart every time the machine restarts.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![sepb-elk successful](https://github.com/rkyletodd/scripts-Project-1/blob/main/diagrams-images/Project_1_sepb_elk.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1 VM 10.0.0.6
- Web2 VM 10.0.0.7
- Web3 VM 10.0.0.9

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Filebeat allows us to collect system logs. Example: Filebeat's elasticsearch module is able to  parse and process the log lines, shaping the data into a structure suitable for visualizing in Kibana.
- Metricbeat monitors and collects system metric information. Example: Metricbeat's elasticsearch module sends metrics to the monitoring index instead of the default index typically used by Metricbeat.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
