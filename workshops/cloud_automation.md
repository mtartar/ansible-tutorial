# Cloud Automation Workshop

## Lab: Infrastructure visibility

### Automation controller

The control plane for Ansible Automation Platform is the automation controller (replacing Ansible Tower).

IMG

Automation controller helps standardize how automation is deployed, initiated, delegated, and audited, allowing enterprises to automate with confidence while reducing sprawl and variance. Manage inventory, launch and schedule workflows, track changes, and integrate into reporting, all from a centralized user interface and RESTful API.

### Inventories

An Inventory is a collection of hosts against which jobs may be launched, the same as an Ansible inventory file. Inventories are divided into groups and these groups contain the actual hosts. Groups may be sourced manually, by entering host names into the automation controller, or from one of its supported cloud providers.

#### Inventory Plugins

There is a variety of pre-built Inventory Plugins that are available:

Amazon Web Services EC2
Google Compute Engine
Microsoft Azure Resource Manager
VMware vCenter


### 

Example of configuring AWS inventory source:


IMG inventories-create-source-AWS-example.png


### Lab Diagram

Here is a diagram of the lab topology.

IMG aws-diagram

There is one automation controller node, and two Red Hat Enterprise Linux nodes running in Amazon Web Services (AWS) Elastic Cloud (EC2).

#### Credentials

Credentials are utilized for authentication when launching Jobs against machines, synchronizing with inventory sources, and importing project content from a version control system. In this lab, we have two different credentials:

RHEL on AWS - SSH KEY - This is an SSH key for the two Red Hat Enterprise Linux hosts running on AWS
aws_credential - This is the AWS credential for performing actions on AWS cloud. For example, creating a VPC, or shutting down an instance.
In the Automation Controller tab at the top of your window click on the Credentials link under Resources to examine the two pre-configured credentials. Login with the credentials provided above.

Note The keys are encrypted so no one, not even an administrator, can see the key once it has been placed in automation controller.
￼


### Understanding Job Templates

A job template is a definition and set of parameters for running an Ansible job. Job templates are useful to execute the same job many times. Job templates also encourage the reuse of Ansible playbook content and collaboration between teams.



https://github.com/ansible-cloud/aws_demos



https://github.com/ansible-cloud/aws_demos/tree/master/roles/build_report

