Variables

In general variables are used to store any values later which are used. 
In ansible variable working is same we cant also store service name that we want to install or start. 

Variables are very useful instead of doing changes in every task simply change the variable value. 

For eg : if you want to install httpd then simply assign it to the variable and use that variable in the playbook rather than giving same value again and again to the task.

There are two types of variables :
1.	Local : These are only accessible within the file 
2.	Global : These are accessible to the multiple files.

Declared local variable

vim httpd.yaml

```
---
- name: installing packages
  hosts: all
  vars:
   - websoft: httpd
  tasks:
   - name: install {{ websoft }}
     yum:
      name: "{{ websoft }}"
      state: latest
   - name: start the {{ websoft }} service
     service:
      name: "{{ websoft }}"
      state: restarted
```

ansible-playbook httpd.yaml


Now execute this playbook and it will be executed without any issues.
coz it is local variable.


In order to use global variable you have to declare it in your inventory file i.e. hosts file where you have added all your servers with this add global variable also.

Eg: hosts  means your inventory file (if you forget means refer your ansible.cfg file)

```
vim hosts

node1
node2

[prod]
node1

[backup]
node2

[all:vars]
websoft=httpd
```

Declare websoft. Here all means it will available to all machines. 
 
Removing the local variable.
 
After executing same output will be there.

You can also restrict the variable for particular machines. 

In the above inventory file we used all to run on all the srver.


```
[prod:vars]
websoft=httpd

save the inventory and exit

Now execute the playbook

ansible-playbook httpd.yaml


you see backup machines will fail
```


However now go to inventory file try the below

```
[backup:vars]
websoft=httpd

save the inventory and exit

Now execute the playbook

ansible-playbook httpd.yaml


you see prod machines will fail

This prove that global variable can be accessiable from any playbook.
```