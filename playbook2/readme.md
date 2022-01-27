Inventory Grouping

node1 --> Dev Group

node2 --> Prod Group

Install httpd in production group of servers only and restart service also in production servers only

vim httpd.yaml
```
---
- name: install httpd
  hosts: prod
  tasks:
   - name: install httpd
     yum:
      name: httpd
      state: latest
   - name: restart web service
     service:
      name: httpd
      state: restarted
```

Install httpd in dev group of servers only and restart service also in dev servers only

vim httpd.yam

```
---
- name: install httpd
  hosts: dev
  tasks:
   - name: install httpd
     yum:
      name: httpd
      state: latest
   - name: restart web service
     service:
      name: httpd
      state: restarted
```

Install httpd in production,dev group of servers and restart service also in both dev & production servers.

vim httpd.yaml

```
---
- name: install httpd
  hosts: prod,dev
  tasks:
   - name: install httpd
     yum:
      name: httpd
      state: latest
   - name: restart web service
     service:
      name: httpd
      state: restarted
```

Install httpd in production group and node2 machine only

vim httpd.yaml


```
---
- name: install httpd
  hosts: prod,node2
  tasks:
   - name: install httpd
     yum:
      name: httpd
      state: latest
   - name: restart web service
     service:
      name: httpd
      state: restarted
```

Install all the plays into all the servers which are listed out in the inventory file.But only one play (or) task must be executed in prod group only

vim httpd.yaml
```
---
- name: install httpd
  hosts: all
  tasks:
   - name: install httpd
     yum:
      name: httpd
      state: latest
     when: inventory_hostname in groups ['prod']
   - name: restart web service
     service:
      name: httpd
      state: restarted

```

Install all the plays into all the servers which are listed out in the inventory file.But only one play (or) task must be executed in prod group and dev group only

````
---
- name: I want to install in prod servers only
  hosts: all
  tasks:
    - name: install httpd
      yum:
        name: httpd
        state: latest
      when: inventory_hostname in groups ['dev']
    - name: restart httpd
      service:
        name: httpd
        state: restarted
      when: inventory_hostname in groups ['prod']
