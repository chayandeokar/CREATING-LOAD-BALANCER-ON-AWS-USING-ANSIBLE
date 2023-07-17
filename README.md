# CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE

What is Load Balancer ?

Load balancing is defined as the methodical and efficient distribution of network or application traffic across multiple servers in a server farm. Each load balancer sits between client devices and backend servers, receiving and then distributing incoming requests to any available server capable of fulfilling them.

So lets start this task.

Create 5 ec2 Instances. Here i am taking mixture of t2.micro and t3.micro. You can take any instance type. But be sure take t3.micro for Ansible Node. In which you have to Install Ansible.

1 - - Ansible Node (Controller Node) -- t3.micro

1 - - LoadBalancer -- t2.micro

3 - - Webserver -- t2.micro

here i have used ansible to launch ec2 instances. code for launching ec2 instance using Ansible.

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/cc29e5c9-27ee-45d1-847e-5a04e131a526)

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/0a1bb463-b081-4594-98ee-f21de02620a2)

Now we have to first create a role inside ControllerNode. Create two roles one for LoadBalancer and another for Webservers.

Set the webservers and loadbalancers inside ansible hosts.

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/82d1fc0d-b89e-420a-9d14-b18e82689b39)


create a role folder mkdir /etc/ansible/roles all the roles will be inside this roles folder.

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/ad9b75d9-3056-4819-a17b-fc046d358d7c)

Also create a directory to manage hosts files. Here i have created

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/14a58df5-99c4-412e-83db-630dac48e1b8)


![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/3d7d17d0-e0e0-4853-8923-aa2aeb0dd4ff)

Also you need to set the path of role inside ansible configuration file (ansible.cfg).

Now we can start writing the playbook inside projects directory.
![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/29dbbd8b-844a-4eab-84e9-a6b593875321)

![image](https://github.com/chayandeokar/CREATING-LOAD-BALANCER-ON-AWS-USING-ANSIBLE/assets/74093567/f8cdeaba-f81c-4112-8a62-2ef550e6ca84)
