# CyberDBHwProj
This is the first Cyber Security Project : Configure ELK Stack.

Getting Started with ELK provides files to ingest, analyze & visualize Apache Access Logs using the ELK stack, i.e. Elasticsearch, Logstash and Kibana and also gives the ability to analyze any data set by using the searching/aggregation capabilities of Elasticsearch and the visualization power of Kibana.

Based on the official Docker images from Elastic:

Elasticsearch
Logstash
Kibana

Run the latest version of the Elastic stack with Docker and Docker Compose.


## Contents
   # - **Diagram** [Refer diagram](../main/Diagrams/ELKProject.png)
   DVWA(Damn Vulnerable Web Application) is hosted and accessed through a LoadBalancer, Loadbalancer is distributing load between 2 virtual machines.
   ELk virtual machine is not directly accessed.
   # - **Steps to set up Elk** [Refer complete setup guide](../main/Resources/Elk%20Commands.pdf)
   Follow the document and make below changes - 
    - Add [install-elk.yml](../main/ConfigFiles/config/install-elk.yml) to 
    etc/ansible
   - Update ansible.cfg remote user, remote_user = sysadmin
   - Updates hosts file - 
            [webservers]
            10.4.0.4 ansible_python_interpreter=/usr/bin/python3
            [elk]
            10.4.0.4 ansible_python_interpreter=/usr/bin/python3
    - Run install-elk.yml file, to configure the ELK to collect logs -  
      cd /etc/ansible
      ansible-playbook install-elk.yml
 
  - Add [filebeat-config.yml](../main/ConfigFiles/config/filebeat-config.yml)and [metricbeat-config.yml](../main/ConfigFiles/config/metricbeat-config.yml) files to 
    etc/ansible/files
  - Add [filebeat-playbook.yml](../main/ConfigFiles/Playbooks/filebeat-playbook.yml) and [metricbeat-playbook.yml](../main/ConfigFiles/Playbooks/metricbeat-playbook.yml) files to 
    etc/ansible/roles
    # - Access Policies 
        The main purpose of this is to monitor DVWA site and to restrict the network attacks. Jumpbox is used to access Virtual Netowrk via ssh.
        Integrating with ELK server allows continuos monitoring of the Virtual Machines traffic. 
        Configurations of each virtual machine -
        
        | Type            | Name                     | IP                       | Publicly Accessible |
        | --------------- | ------------------------ | ------------------------ | ------------------- |
        | Virtual Machine | vm-webserver1-useast-011 | 10.2.0.6(Private IP)     | No                  |
        | Virtual Machine | vm-webserver2-useast-011 | 10.2.0.5(Private IP)     | No                  |
        | Virtual Machine | vm-jumpbox-useast-011    | 13.68.148.102(Public IP) | Yes                 |
        | Virtual Machine | vm-elkhost-011           | 10.4.0.4(Private IP)     | No                  |

  vm-elkhost-011 is configured to monitor vm-webserver1-useast-011 and vm-webserver2-useast-011.
  Elk host has Filebeat and Metricbeat running, filebeat collects log data and shows them in the monitoring clusters and metricbeat collects metrics and statistics and shows them in the output specified, for example Elasticsearch or Logstash. 
  Link to check logs once successfully configured - http://<IP>:5601/app/kibana
  Check the detailed logs, 
   [FilebeatLogs](../main/LogFiles/FilebeatLogs.pdf)
   [MetricbeatLogs](../main/LogFiles/MetricbeatLogs.pdf)
   
   Also can customize logs by providing different time ranges and other options.
  
   Additional  [resources](../main/Resources) are added incase of any issues.

