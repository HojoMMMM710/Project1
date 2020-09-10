# Project1
Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _ file may be used to install only certain pieces of it, such as Filebeat.
TODO: Enter the playbook file. ---
- name: installing and launching filebeat
  hosts: webservers
  become: yes
  tasks:


  - name: download filebeat deb
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7$


  - name: install filebeat deb
    command: sudo dpkg -i filebeat-7.6.1-amd64.deb


  - name: drop in filebeat.yml
    copy:
    #src: ./filebeat.yml
      src: /etc/filebeat/filebeat.yml
      dest: /etc/filebeat/filebeat.yml


  - name: enable and configure system module
    command: sudo filebeat modules enable system


  - name: setup filebeat
    command: sudo filebeat setup


  - name: start filebeat service
    command: sudo service filebeat start
This document contains the following details:
Description of the Topologu
Access Policies
ELK Configuration
Beats in Use
Machines Being Monitored
How to Use the Ansible Build
Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly stable, in addition to restricting traffic to the network.
TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?
Load balancers play an important role in the aspect of security with it’s off-loading function that can defend against DDos attacks. With this function of load balancers they play an important role for corporations because they are efficient and cost-effective protection. The advantage of using a jumpbox is the fact that all admins connect to a secure computer before administering a task while managing devices in a separate security zone. The jumpbox is hardened and monitored that device and provides a controlled means of access between other servers. 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system files.
TODO: What does Filebeat watch for? File beat watches for log files or a location that we specify, collects log events, and forwards these into Elasticsearch or Logstash.
TODO: What does Metricbeat record? Metricbeat records metrics and statistics and chips them to the output that we specify, such as Elasticsearch or Logstash. An example of the collected metrics from the system and services running is Apache.
The configuration details of each machine may be found below.
Note: Use the Markdown Table Generator to add/remove values from the table.
Name
Function
IP Address
Operating System
Jump Box
Gateway
10.0.0.4
Linux
Elk-VM
Server
10.1.0.4
Linux
Web1 
Server
10.0.0.5
Linux
Web2
Server 
10.0.0.6
Linux
Web3
Server 
10.0.0.7
Linux 
Access Policies
The machines on the internal network are not exposed to the public Internet.
Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
173.61.27.184
Machines within the network can only be accessed by SSH.
TODO: Which machine did you allow to access your ELK VM? What was its IP address? The machine I allowed access to my ELK VM was my workstation computer. The IP address for this machine is 173.61.27.184.
A summary of the access policies in place can be found in the table below.
Name
Publicly Accessible
Allowed IP Addresses
Jump Box
Yes/No
10.0.0.1 10.0.0.2












Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
TODO: What is the main advantage of automating configuration with Ansible? The main advantage to using automating configuration with Ansible is the fact that we do not need to manually write custom code, the ansible will figure out how to get the system to where we want it to be through writing a playbook. 
The playbook implements the following tasks:
TODO: In 3-5 bullets, explain the steps of the ELK installation play.
 The playbook will launch and install filebeat
First it will DOwnload and install filebeat 
Next it will copy and place the configuration file we made into the proper destination 
Next it will enable and configure the system module
Finally, it will setup and launch filebeat
The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.
![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

Target Machines & Beats
This ELK server is configured to monitor the following machines:
TODO: List the IP addresses of the machines you are monitoring
10.0.0.5, 10.0.0.6, 10.0.0.7
We have installed the following Beats on these machines:
TODO: Specify which Beats you successfully installed
Filebeat7.6.1 was installed on these machines
These Beats allow us to collect the following information from each machine:
TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., Winlogbeat collects Windows logs, which we use to track user logon events, etc.
Filebeat collects log files, log events, and forwards them to Elasticsearch and Logstash. A log file is a computer-generated file and it contains usage patterns, activities, and operations within an operating system, application, server, or another device.
Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:
Copy the filebeat.yml(filebeat config file) file to filebeat-playbook.yml.
Update the filebeat-playbook.yml file to include the copying of the config file to the destination of /etc/filebeat/filebeat.yml
Run the playbook, and navigate to http://52.173.32.157:5601/app/kibana#/home/tutorial/systemLogs to check that the installation worked as expected.
TODO: Answer the following questions to fill in the blanks:
Which file is the playbook? Where do you copy it? The playbook file is /etc/ansible/roles/filebeat-playbook.yml. You copy the filebeat.yml file to /etc/filebeat/filebeat.yml
Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? We have to update the /etc/ansible/hosts files to configure which machines we want to add to webservers and update the playbook to download and install filebeat on the webservers. To specify which machine to install the ELK server on versus which to install filebeat on, we have to configure the /etc/ansible/hosts file and the playbook we use to download ELK and filebeat.
_Which URL do you navigate to in order to check that the ELK server is running?
We navigate to http://52.173.32.157:5601/app/kibana  to check that the ELK server is running.
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._ 
ansible-playbook filebeat-playbook.yml 
