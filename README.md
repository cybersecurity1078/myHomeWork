## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)
/Users/bridgetoperu/Desktop/diagram

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ___ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._
Configure Elk VM with Docker
  hosts: elk
  remote_user: azadmin
  become: true
  tasks:
    # Use apt module
    - name: Install docker.io
      apt:
        update_cache: yes
        name: docker.io
        state: present

      # Use apt module
    - name: Install pip3
      apt:
        force_apt_get: yes
        name: python3-pip
        state: present

      # Use pip module
    - name: Install Docker python module
      pip:
        name: docker
        state: present

      # Use sysctl module
    - name: Use more memory
      sysctl:
        name: vm.max_map_count
        value: "262144"
        state: present
        reload: yes

      # Use docker_container module
    - name: download and launch a docker elk container
      docker_container:
        name: elk
        image: sebp/elk:761
        state: started
        restart_policy: always
        published_ports:
          - 5601:5601
          - 9200:9200
          - 5044:5044

      # Use systemd module
    - name: Enable service docker on boot
      systemd:
        name: docker
        enabled: yes
This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
The off-loading function of a load balancer defends an organization against DDoS Attacks.Distributing Network traffic across multiple servers. 
A Jump Box is a Hardened server that you jump in order to access other servers via SSH in a more protected network.  

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_is a lightweight  shipper for forwarding and centralizing data.Monitors the log files or that you specify location. 
- _TODO: What does Metricbeat record?_is a lightweight  shipper that you can install on your server  to periodically collect metrics from the operating system and from services running on the server.
The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| TODO     |          |            |                  |
| TODO     |          |            |                  |
| TODO     |          |            |                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_157.56.177.52

Machines within the network can only be accessed by _____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
Jump Box 157.56.177.52
A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.1 10.0.0.2    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
Create a new virtual network in a different region , create a peer connection between the 2 vNets.create a new VM ELK, with more than 4 GiB of memory for the ELK container,The VM must have a Public IP,allow a new Security Group,the VM music use the same SSH Keys  as the Web VM the SSH key created on the Ansible container that's  running on the jump box, from the terminal SSH into the Jump Box,from the Jump Box login shell attach to the ainsible container, use cat to the public ssh key, configure the container , create a playbook that install docker and configures the container.verify access your server navigating to Kibana.
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.



![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
https://ucb.bootcampcontent.com/UCB-Coding-Bootcamp/ucb-virt-cyber-pt-06-2021-u-lol/-/raw/master/13-Elk-Stack-Project/Activities/Stu_Day_1/Unsolved/Resources/Kibana_Home.png
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
Web-1 10.0.0.5
Web-2 10.0.0.6
ELK. 10.2.0.4
We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

Filebeat,Metricbeat
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat.-monitors the log files or locations that you specify collects logs events.
Metricbeat.-takes the metrics and statistics that it collects.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_they are collections of procedures that can be run from azure.copy it in the ainsible machine.
- _Which file do you update to make Ansible run the playbook on a specific machine?
 How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._