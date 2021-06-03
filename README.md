## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/78666640/119899786-97f99e80-bf11-11eb-854f-f1cc42880337.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  /etc/ansible/files/filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting traffic to the network.
- A load balancer restricts access while distributing network traffic across servers. This can help protect against DDoS attacks. 
- A jumpbox serves as a secure node from which an adminstrator can connect to other systems.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- Filebeat collects logs about the file system, watching for changes made to files and when they were made.
- Metricbeat records various metrics of a system such as CPU usage and uptime. 

The configuration details of each machine may be found below.

| Name    | Function | IP Address | Operating System |
|---------|----------|------------|------------------|
| Jumpbox | Gateway  | 10.0.0.4   | Linux            |
| Web 1   | Server   | 10.0.0.9   | Linux            |
| Web 2   | Server   | 10.0.0.8   | Linux            |
| ELK     | Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 136.55.85.135

Machines within the network can only be accessed by the Jumpbox.
- Jumpbox. 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump Box   | Yes                 | 52.136.112.37        |
| Web 1 DVWA | No                  | 10.0.0.9             |
| Web 2 DVWA | No                  | 10.0.0.8             |
| ELK Server | No                  | 10.1.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- the playbook efficiently encompasses all configuration aspects and streamlines the process, minimizing the likelihood of human error.

The playbook implements the following tasks:
- Installs docker.io
- Installs pip3
- Installs Docker python module
- Increases virtual memory
- Downloads and launches docker ELK container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/78666640/119903484-c332bc80-bf16-11eb-8af9-8c943cfffbcd.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web 1 (10.0.0.9)
- Web 2 (10.0.0.8)

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects data about the file system, specifically looking for things like when and what files have changed. These log files are sent to Logstash and Elasticsearch.
- Metricbeat collects machine metrics and statistics. Some examples would include uptime and CPU usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible/files.
  - filebeat-playbook.yml
  - Copy to /etc/ansible/files

- Update the hosts file to include allowed IPs
  - /etc/ansible/hosts
  - Update the above file to add the [elk] group and the allowed IP address (10.1.0.4)
 
- Run the playbook, and navigate to the web server to check that the installation worked as expected.
  - http://[your.VM.IP]:5601/app/kibana
