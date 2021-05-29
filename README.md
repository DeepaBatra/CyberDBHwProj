# CyberDBHwProj
This is the first Cyber Security Project : Configure ELK Stack.

Getting Started with ELK provides files to ingest, analyze & visualize Apache Access Logs using the ELK stack, i.e. Elasticsearch, Logstash and Kibana and also gives the ability to analyze any data set by using the searching/aggregation capabilities of Elasticsearch and the visualization power of Kibana.

Based on the official Docker images from Elastic:

Elasticsearch
Logstash
Kibana

Run the latest version of the Elastic stack with Docker and Docker Compose.


## Contents
   # - **Diagram** [Refer diagram](../blob/main/Diagrams/ELKProject.png)
   DVWA(Damn Vulnerable Web Application) is hosted and accessed through a LoadBalancer, Loadbalancer is distributing load between 2 virtual machines.
   ELk virtual machine is not directly accessed.
   # - **Steps to set up Elk** [Refer complete setup guide](../blob/main/Resources/Elk%20Commands.pdf)
   Follow the document and make below changes - 
    - Add [install-elk.yml](../blob/main/ConfigFiles/config/install-elk.yml) to 
    etc/ansible
   - Update ansible.cfg remote user, remote_user = sysadmin
   - Updates hosts file - 
            [webservers]
            10.4.0.4 ansible_python_interpreter=/usr/bin/python3
            [elk]
            10.4.0.4 ansible_python_interpreter=/usr/bin/python3
 
  - Add [filebeat-config.yml](../blob/main/ConfigFiles/config/filebeat-config.yml)and [metricbeat-config.yml](../https://github.com/DeepaBatra/CyberDBHwProj/blob/main/ConfigFiles/config/metricbeat-config.yml) files to 
    etc/ansible/files
  - Add [filebeat-playbook.yml](../blob/main/ConfigFiles/Playbooks/filebeat-playbook.yml) and [metricbeat-playbook.yml](../blob/main/ConfigFiles/Playbooks/metricbeat-playbook.yml) files to 
    etc/ansible/roles
    # - Access Policies 
        The main purpose of this is to monitor DVWA site and to restrict the network attacks. Jumpbox is used to access Virtual Netowrk via ssh.
        Integrating with ELK server allows continuos monitoring of the Virtual Machines traffic. Configurations of each virtual machine -
        
        | Type            | Name                     | IP                   | Publicly Accessible |
        | --------------- | ------------------------ | -------------------- | ------------------- |
        | Virtual Machine | vm-webserver1-useast-011 | 10.2.0.6(Private IP) | No                  |

  
    

