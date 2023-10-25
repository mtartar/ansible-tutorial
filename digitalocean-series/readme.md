# Ansible

- [How To Write Ansible Playbooks](https://www.digitalocean.com/community/tutorial-series/how-to-write-ansible-playbooks)

## Creating and Running your First Ansible Playbook


```
ansible-playbook -i inventory playbook-01.yml -u sammy
```


## How To Define Tasks in Ansible Playbooks

Tasks are defined as a list under the name tasks inside a play,
at the same level as the hosts directive that defines the targets for that play.

The name property defines the output that will be printed out when that task is about to be executed.

The example task invokes the debug module, which allows you to display messages in a play.

Each module has its own set of options and properties.
The debug module expects a property named msg containing the message to be printed out.


## How To Use Variables in Ansible Playbooks

[Special precedence rules](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable)


```
ansible-playbook -i inventory playbook-02.yml -u sammy
```

## How To Access System Information (Facts) in Ansible Playbooks


```
ansible all -i inventory -m setup -u sammy
```

```
ansible all -i inventory -m setup -a "filter=*ipv4*" -u sammy 
```


```
ansible-playbook -i inventory playbook-03.yml -u sammy
```


## How To Use Conditionals in Ansible Playbooks


```
ansible-playbook -i inventory playbook-04.yml -u sammy
```

```
ansible-playbook -i inventory playbook-05.yml -u sammy
```


## How To Use Loops in Ansible Playbooks


```
ansible-playbook -i inventory playbook-06.yml -u sammy
```


## Understanding Privilege Escalation in Ansible Playbooks


```
ansible-playbook -i inventory playbook-07.yml -u sammy -K

```


The ansible_env.USER fact contains the username of the connecting user,
which can be defined at execution time when running the ansible-playbook command with the -u option.


```
ansible-playbook -i inventory playbook-08.yml -u sammy -K
```


## How To Install and Manage System Packages in Ansible Playbooks


```
ansible-playbook -i inventory playbook-09.yml -u sammy -K
```



```
ansible-playbook -i inventory playbook-10.yml -u sammy -K
```


## How To Create and Use Templates in Ansible Playbooks

```
ansible-playbook -i inventory playbook-11.yml -u sammy -K
```


## How To Define and Use Handlers in Ansible Playbooks

```
ansible-playbook -i inventory playbook-12.yml -u sammy -K
```

http://127.0.0.1/


## How To Deploy a Static HTML Website with Ansible on Ubuntu 20.04 (Nginx)

...