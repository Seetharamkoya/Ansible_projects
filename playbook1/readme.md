Handler :

Sometimes you want a task to run only when a change is made on a machine. 
For example, you may want to restart a service if a task updates the configuration of that service, but not if the configuration is unchanged. Ansible uses handlers to address this use case. Handlers are tasks that only run when notified.

What are the tags in Ansible?

Image result for tags in ansible
A tag is an attribute that you can set to an Ansible structure (plays, roles, tasks), and then when you run a playbook you can use –tags or –skip-tags to execute a subset of tasks.


commands:

tags

To list all the tags in our playbook

> ansible-playbook <playbook name>  --list-tags


To run our own tasks with --tag=task name/tag name

> ansible-playbook <playbook name>   --tags 

To list the list of tasks in our playbook

> ansible-playbook <playbook name>   --list-tasks

To skip the some of the tags while running

> ansible-playbook <playbook name>   --skip-tags

To take yes or No decision for each task or play in our playbook

> ansible-playbook <playbook name>  --step