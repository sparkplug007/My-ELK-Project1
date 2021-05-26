# My-ELK-Project1
ELK project set-up and submission
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
![alt-txt](https://github.com/sparkplug007/My-ELK-Project1/blob/main/Diagrams/Cloud%20Diagram_with_ELK.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the *.yml* file may be used to install only certain pieces of it, such as Filebeat.

 - [Configure ELK-VM](https://github.com/sparkplug007/My-ELK-Project1/blob/867fee882ea9228db0516ec585ba15d09f645b8c/Ansible/install-elk.yml)
 - [DVWA configuration](https://github.com/sparkplug007/My-ELK-Project1/blob/main/Ansible/firstactivity.yml)
 - [filebeat.config file](https://github.com/sparkplug007/My-ELK-Project1/blob/main/Ansible/filebeat-config.yml)
 - [metricbeat.config file](https://github.com/sparkplug007/My-ELK-Project1/blob/main/Ansible/metricbeat-config.yml)
 - [filebeat playbook](https://github.com/sparkplug007/My-ELK-Project1/blob/867fee882ea9228db0516ec585ba15d09f645b8c/Ansible/filebeat-playbook.yml)
 - [metricbeat playbook](https://github.com/sparkplug007/My-ELK-Project1/blob/867fee882ea9228db0516ec585ba15d09f645b8c/Ansible/metricbeat-playbook.yml)

This document contains the following details:
 - Description of the Topology
 - Access Policies
 - ELK Configuration
 - Beats in Use
 - Machines Being Monitored
 - How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Load balancers protects and restrict access and ensure availabilty to all of my webservers which is one of the pillar in the CIA triad. What is the advantage of a jump box? Having a (dedicated) Jump-box ensures a secure access point to do administrative tasks
in configuring webservers for deployment. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.
- Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function                   | IP Address       | Operating System        |
|----------|----------------------------|------------------|-------------------------|
| Jump-Box Provisioner | Gateway        | 10.0.0.1         | Linux Ubuntu 18.04-LTS  |
| web-1    | webserver-DVWA             | 10.0.0.6         | Linux Ubuntu 18.04-LTS  |
| web-2    | webserver-DVWA             | 10.0.0.7         | Linux Ubuntu 18.04-LTS  |
| ELK-server|ELK-stack                  | 10.1.0.4         | Linux Ubuntu 18.04-LTS  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box Provisioner and ELK-server machines can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 10.0.0.4 internal IP address
- 10.1.0.4 internal IP address

Machines within the network can only be accessed by ssh.
- ELK-server VM can only be access through ssh from my Jump-Box Provisioner via my 10.1.0.4 internal IP address

A summary of the access policies in place can be found in the table below.

| Name                  | Publicly Accessible | Allowed IP Addresses     |
|-----------------------|---------------------|--------------------------|
| Jump Box Provisioner  | Yes                 | my Box-public IP address |
| web-1                 | No                  | 10.0.0.4 private IP address|
| web-2                 | No                  | 10.0.0.4 private IP address|
| ELK-server            | Yes                 | my Box-public IP address |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because when deploying multiple servers you have to be deligent especially on your inputs, it is fast and not labor intensive compare to manually and individual working on each box, this task is enormous when dealing with hundreds of servers to configurre.

With having a playbook to implement for deployment, with this configuration, it can also be easily modified whatever tasks your job need:
- Install or Uninstall a webserver
- Install docker.io and python3-pip packages with apt module
- Install docker python package with pip
- Configure maximum mapped memory with sysctl module
- Enable sysctl module
- Enable systemd module
- Sets published ports

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt-txt](https://github.com/sparkplug007/My-ELK-Project1/blob/main/Images/docker%20ps%20-a%20command.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- web-1 ( local IP 10.0.0.6 )
- web-2 ( local IP 10.0.0.7 )

We have installed the following Beats on these machines:
- filebeat
- metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat is a lightweight shipper for forwarding and centralizing log data. Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash and Kibana for indexing.
- Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch, Logstash or Kibana.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files folder.
- Update the filebeat-config.yml file to include the private IP of the ELK-server (10.1.0.4) to the hosts in output:elasticsearch and setup.kibana section of the configuration file.
- Repeat this procedure for the metricbeat-config.yml file.
- Run the playbook, _$ ansible-playbook filebeat-playbook.yml_

![alt-txt](https://github.com/sparkplug007/My-ELK-Project1/blob/main/Images/ansible-playbook_filebeat.png)

and navigate to http://[ELK-server Public IP]:5601/app/kibana. to check that the installation worked as expected.

![alt-txt](https://github.com/sparkplug007/My-ELK-Project1/blob/main/Images/ELK-filebeat-kibana.png)

Which file is the playbook:
- _first activity.yml_ - used to configured dockers on DVWA was copied to /etc/ansible folder
- _install-elk.yml_ - used to install my ELK-server was copied to /etc/ansible/files folder
- _filebeat-playbook.yml_ - used to configured filebeat was copied to /etc/ansible/roles folder
- _metricbeat-playbook.yml_ - used to configured metricbeat was copied to /etc/ansible/roles folder

Which file do you update to make Ansible run the playbook on a specific machine?
- /etc/ansible/hosts

![alt-txt](https://github.com/sparkplug007/My-ELK-Project1/blob/main/Images/host.png)

How do I specify which machine to install the ELK server on versus which to install Filebeat on?
As shown above, navigate to the _**/etc/ansible/hosts**_ file and add which machine you need to add while
filebeat is a logging agent installed on the server machine generating the log files.

Which URL do you navigate to in order to check that the ELK server is running?

![alt-txt](https://github.com/sparkplug007/My-ELK-Project1/blob/main/Images/ELK-filebeat-kibana.png)

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

![alt-txt](https://github.com/sparkplug007/My-ELK-Project1/blob/main/Images/docker%20ps%20-a%20command.png)

After identifying that the ansible are running in you machine, activate the shell container to get connected to it
Navigate to _**/etc/ansible/**_ folder and copy all youy *.yml* files and edit these files to want you need to accomplish.

![alt-txt](https://github.com/sparkplug007/My-ELK-Project1/blob/main/Images/bonus.png)

