# Ansible

## First playbook

Ansible navigator is a command based tool for creating, reviewing and troubleshooting Ansible content. This includes inventories, playbooks, and collections.


### Inventory

An inventory file is a text file that specifices the nodes that will be managed by the control machine. The nodes to be managed may include a list of hostnames or IP addresses of those nodes. The inventory file allows for nodes to be organized into groups by declaring a host group name within square brackets ([]).


An example inventory:

```
[all:vars]
ansible_user=rhel
ansible_password=SomethingSomething
ansible_port=22

[web]
websrv1
websrv2

[db]
db_1 ansible_host=11.22.33.44
db_2 ansible_host=44.55.66.77
```

- Create file `hosts`

```
[web]
node1
node2
```


- Check inventory

```
ansible-navigator inventory --list
```

or 

```
ansible-navigator inventory --graph
```


### Playbook

Playbooks are files which describe the desired configurations or steps to implement on managed hosts. Playbooks can change lengthy, complex administrative tasks into easily repeatable routines with predictable and successful outcomes.

A playbook can have multiple plays and a play can have one or multiple tasks. In a task, a module is called to run an action against. The goal of a play is to map a group of hosts. The goal of a task is to implement modules against those hosts.

￼
Playbooks are text files written in YAML format and therefore need:
- to start with three dashes (---)
- proper indentation using spaces and not tabs!


There are some important concepts:
- `hosts`: the managed hosts to perform the tasks on
- `tasks`: the operations to be performed by invoking Ansible modules and passing them the necessary options.
- `become`: privilege escalation in Playbooks, same as using `-b` in the ad hoc command.

Good Playbooks are idempotent, so if a Playbook is run once to put the hosts in the correct state, it should be safe to run it a second time and it should make no further changes to the hosts.



- Write playbook `apache.yml`

```
- name: Apache server installed
  hosts: node1
  become: true
  tasks:
  - name: latest Apache version installed
    ansible.builtin.package:
      name: httpd
      state: latest
```



- Verify that Apache is installed

```
ansible node1 -m ansible.builtin.shell -a "rpm -qi httpd"
```


By default, Ansible executes each task in order, one at a time, against all machines matched by the host pattern. Each task executes a module with specific arguments. When a task has executed on all target machines, Ansible moves on to the next task.




- Update playbook `apache.yml`

```
---
- name: Apache server installed
  hosts: node1
  become: true
  tasks:
  - name: latest Apache version installed
    ansible.builtin.package:
      name: httpd
      state: latest
  - name: Apache enabled and running
    ansible.builtin.service:
      name: httpd
      enabled: true
      state: started
```


- Verify status of Apache

```
ansible node1 -m ansible.builtin.service_facts | grep httpd.service -A 4
```



### Variables

Ansible supports variables to store values that can be used in Playbooks. Variables can be defined in a variety of places and have a clear precedence. Ansible substitutes the variable with its value when a task is executed.

￼
Variables are referenced in Ansible Playbooks by placing the variable name in double curly braces:

Here comes a variable `{{ variable1 }}`


Variables and their values can be defined in various places: the inventory, additional files, on the command line, etc.


The recommended practice to provide variables in the inventory is to define them in files located in two directories named `host_vars` and `group_vars`:

- To define variables for a group “servers”, a YAML file named `group_vars/servers.yml` with the variable definitions is created.
- To define variables specifically for a host node1, the file `host_vars/node1.yml` with the variable definitions is created.


Host variables take precedence over group variables (more about precedence can be found in the [docs](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable)).


### Conditions


In a playbook, you can use Ansible conditionals to execute tasks or plays when certain conditions are met. To implement a conditional, the `when` statement must be used, followed by the condition to test. The condition is expressed using one of the available operators like

- `==`	Compares two objects for equality.
- `!=`	Compares two objects for inequality.
- `>`	true if the left hand side is greater than the right hand side.
- `>=`	true if the left hand side is greater or equal to the right hand side.
- `<`	true if the left hand side is lower than the right hand side.
- `<=`	true if the left hand side is lower or equal to the right hand side.

￼

### Loops

Loops enable us to repeat the same task over and over again. For example, lets say you want to create multiple users. By using an Ansible loop, you can do that in a single task.

Loops can also iterate over more than just basic lists. For example, if you have a list of users with their corresponding group, loop can iterate over them as well.


### Handlers

Handlers can be seen as inactive tasks that only get triggered when explicitly invoked using the "notify" statement.


### Templates

Ansible uses [Jinja2](http://jinja.pocoo.org) templating to modify files before they are distributed to managed hosts. Jinja2 is one of the most used template engines for Python.

A typical ending for a file to indicate that it is a template file is `.j2`. Though this is strictly speaking not necessary, it is established practice.



### Roles

An Ansible role has a defined directory structure with eight main standard directories. You must include at least one of these directories in each role. You can omit any directories the role does not use.

By default Ansible will look in each directory within a role for a main.yml file for relevant content.


mkdir roles

ansible-galaxy init --offline roles/apache_vhost


### Doc

ansible-doc ansible.builtin.get_url

