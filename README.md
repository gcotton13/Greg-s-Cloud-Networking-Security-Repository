# Greg-s-Cloud-Networking-Security-Repository
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![My Network Topology](Diagrams/Cloud-Security-Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

- [DVWA Webserver Playbook](/etc/ansible/ansible-activityplaybook.yml)
- [ELK Stack Playbook](/etc/ansible/install-elk.yml)
- [Filebeat Playbook](/etc/ansible/filebeat-playbook.yml)
- [Metricbeat Playbook](/etc/ansible/metricbeat-playbook.yml)

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

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.

A Filbert is used for forwarding a centralizing log data.
MetricBeat takes the metrics and statistics that it collects and ships them to the output that you specify.
The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    |App Server| 10.0.0.5   | Linux            |
| Web-2    |App Server| 10.0.0.6   | Linux            |
| Elk-stack|Elk-Stack | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner and ELK Stack (Kibana) machines can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
My Home IP Address


Machines within the network can only be accessed by Jump-Box-Provisioner.


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | My Home IP Address   |
| Elk-stack| Yes                 | My Home IP Address   |
| Web-1    | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because because it allows a consistent and predictable configuration. In addition to consistency, with an automated setup, the ELK stack can be created and configured very quickly.


The playbook implements the following tasks:
-Configure maximum mapped memory with sysctl module
-Install docker.io and python3-pip packages with apt module
-Install docker python package with pip
-Enable systemd docker service
-Run ELK docker container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![output-docker-ps](Ansible/output-docker-ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.5
- Web-2: 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat parses and forwards system logs from the Web VMs to the ELK Stack in an easy to read format.
- Metricbeat reports system and service statistics about the Web VMs to the ELK stack VM.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the 'install-elk.yml file to '/etc/ansible'
	directory inside the ansible container.
- Update the [/etc/ansible/hosts](Ansible/hosts) file to include the ELK stack VM IP address.
  - Append `ansible_python_interpreter=/usr/bin/python3` to ensure that the
      correct version of python is used.
    - Example configuration of `/etc/ansible/hosts`
```bash
[elk]
<internal.ip>      ansible_python_interpreter=/usr/bin/python3
<external.ip>      ansible_python_interpreter=/usr/bin/python3
alpha.example.org  ansible_python_interpreter=/usr/bin/python3

- Run the playbook, and navigate to 'http://[your.elk.ip]:5601/app/kibana.' to check that the installation worked as expected.


-The playbook are the files where Ansible code is written.
-You have to update a playbook and inventory file to make the playbook run on a specific machine.
