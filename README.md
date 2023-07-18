# CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE

## What is Load Balancer ?

** Load balancing is defined as the methodical and efficient distribution of network or application traffic across multiple servers in a server farm. Each load balancer sits between client devices and backend servers, receiving and then distributing incoming requests to any available server capable of fulfilling them. **

## So lets start this task.

## Create 5 ec2 Instances. Here i am taking mixture of t2.micro and t3.micro. You can take any instance type. But be sure take t3.micro for Ansible Node. In which you have to Install Ansible.

> Ansible Node (Controller Node) -- t3.micro

> LoadBalancer -- t2.micro

> Webserver -- t2.micro

## Here i have used ansible to launch ec2 instances. code for launching ec2 instance using Ansible.

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/cc29e5c9-27ee-45d1-847e-5a04e131a526)

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/0a1bb463-b081-4594-98ee-f21de02620a2)

## Now we have to first create a role inside ControllerNode. Create two roles one for LoadBalancer and another for Webservers.

## Set the webservers and loadbalancers inside ansible hosts.

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/82d1fc0d-b89e-420a-9d14-b18e82689b39)

## create a role folder mkdir /etc/ansible/roles all the roles will be inside this roles folder.

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/ad9b75d9-3056-4819-a17b-fc046d358d7c)

## Also create a directory to manage hosts files. Here i have created

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/14a58df5-99c4-412e-83db-630dac48e1b8)
![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/3d7d17d0-e0e0-4853-8923-aa2aeb0dd4ff)

## Also you need to set the path of role inside ansible configuration file (ansible.cfg).

## Now we can start writing the playbook inside projects directory.
![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/29dbbd8b-844a-4eab-84e9-a6b593875321)

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/f8cdeaba-f81c-4112-8a62-2ef550e6ca84)

## After that we have to configure webserver of each instance. We have write the tasks in tasks folder and handlers in handlers folder.

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/5dd60730-ced0-482f-9aca-9228c1a527cd)

## Now we can write the tasks inside main.yml.

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/c0530908-4aaf-477f-a436-d4a892a5d4cb)

## Here we have completed with configuring webserver. You can also use Handlers to restart apache server. Now we have to configure the Load Balancer. First install haproxy inside Controller node.

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/e758027e-bd0f-4bf8-b96c-43b9467df12e)

## Then you need to change the port number binding. You can use any port eg 1234. Here i have used 8080. also you need to provide the public ip of all the instances with 80 port. To give Ip randomly here we can use Jinja Template to extract the hostname of each ec2 instance.

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/59304057-f1d3-4a85-a814-ea64d5ba854a)

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/649d85af-8e03-46be-8b76-8f7c2d2e9906)

## Now go to configuration file of haproxy -- > /etc/haproxy/haproxy.cfg and copy the haproxy.cfg and paste inside /etc/ansible/roles/lbserver/templates. You can also give the location of configuration file of haproxy.

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/25e068e4-4d8f-4098-a764-24c40a00f4c5)

## Now we are ready to run the ansible-playbook. go inside /etc/ansible/roles/projects.From here we can run the play book.

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/f4972821-0ced-4374-ba2d-6481f68ef962)

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/64dbc850-0d76-440e-87b3-84960aeed404)

** Now we can check the weather our load balancer is working or not. Take public IP of load balancer with port 8080 (binding port) **
