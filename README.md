# My-ELK-Project1
ELK project set-up and submission
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
![alt-txt](https://github.com/sparkplug007/My-ELK-Project1/blob/main/Diagrams/network_diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

 - [Configure ELK-VM](https://github.com/sparkplug007/My-ELK-Project1/blob/867fee882ea9228db0516ec585ba15d09f645b8c/Ansible/install-elk.yml)
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
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

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
- ELK-server VM can only be access through ssh from my Jump-Box Provisioner via my 10.0.0.4 internal IP address

A summary of the access policies in place can be found in the table below.

| Name                  | Publicly Accessible | Allowed IP Addresses     |
|-----------------------|---------------------|--------------------------|
| Jump Box Provisioner  | Yes                 | my Box-public IP address |
| web-1                 | No                  | 10.0.0.4 private IP address|
| web-2                 | No                  | 10.0.0.4 private IP address|
| ELK-server            | Yes                 | my Box-public IP address |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.








![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

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
