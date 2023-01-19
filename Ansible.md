1. What is Ansible?
Ansible is a configuration management system. It is used to set up and manage infrastructure and applications. It allows users to deploy and update applications using SSH, without needing to install an agent on a remote system.

2. What is the use of Ansible?
Ansible is used for managing IT infrastructure and deploying software apps5. What is Ansible Galaxy? to remote nodes. Ansible allows you to deploy an application to many nodes with one single command. However, for that, there is a need for some programming knowledge to understand the Ansible scripts.

3. What are the features of Ansible?
Ansible has the following features:

Agentless: Unlike Puppet or Chef, there is no software or agent managing the nodes
Python: Built on top of Python, which is very easy to learn and write scripts. It is one of the robust programming languages. Python Programming Course is one of the most demanding skills right now in the market.
SSH: Passwordless network authentication makes it more secure and easy to set up
Push architecture: The core concept is to push multiple small codes to configure and run the action on client nodes
Set up: This is very easy to set up with a very low learning curve. It is open-source; so, anyone can access it.
Manage inventory: Machines’ addresses are stored in a simple text format and we can add different sources of truth to pull the list using plug-ins such as OpenStack, Rackspace, etc.

Ansible can communicate with configured clients from the command line by using the Ansible command. It also allows you to automate configuration by using the Ansible-playbook command. To create the base directory structure, you can use a tool bundled with Ansible, which is known as ansible-galaxy

6. What is CI/CD?
Continuous integration is something that is used for streamlining the development and deployment process. This has led to the more rapid development of cohesive software. Each integration is verified by an automated build to detect integration errors as quickly as possible.

Continuous delivery is the process where your code after being pushed to a remote repository can be taken to production at any time. It is, in simpler words, a process where you build software in such a way that it can be released to production at any time.

7. What is configuration management?
It is a practice that we should follow in order to keep track of all updates that are going into the system over a period of time. This also helps in a situation where a major bug has been introduced to the system due to some new changes that need to be fixed with minimum downtime. Configuration management (CM) keeps a track of all updates that are needed in a system and it ensures that the current design and build state of the system is up to date and functioning correctly.

9. What are Ansible tasks?
The task is a unit action of Ansible. It helps by breaking a configuration policy into smaller files or blocks of code. These blocks can be used in automating a process. For example, to install a package or update a software:

Command: Install <package_name>

Command: update <software_name>

10. Explain a few of the basic terminologies or concepts in Ansible
A few of the basic terms that are commonly used while operating on Ansible are:

Controller machine: The controller machine is responsible for provisioning servers that are being managed. It is the machine where Ansible is installed.
Inventory: An inventory is an initialization file that has details about the different servers that you are managing.
Playbook: It is a code file written in the YAML format. A playbook basically contains the tasks that need to be executed or automated.
Task: Each task represents a single procedure that needs to be executed, e.g., installing a library.
Module: A module is a set of tasks that can be executed. Ansible has hundreds of built-in modules but you can also create custom ones.
Role: An Ansible role is a predefined way for organizing playbooks and other files in order to facilitate sharing and reusing portions of provisioning.
Play: A task executed from start to finish or the execution of a playbook is called a play.
Facts: Facts are global variables that store details about the system such as network interfaces or operating systems.
Handlers: Handlers are used to trigger the status of a service such as restarting or stopping a service

11. What is a playbook?
A playbook has a series of YAML-based files that send commands to remote computers via scripts. Developers can configure complete complex environments by passing a script to the required systems rather than using individual commands to configure computers from the command line remotely. Playbooks are one of Ansible’s strongest selling points and are often referred to as Ansible’s building blocks.

13. Where are tags used?
A tag is an attribute that sets the Ansible structure, plays, tasks, and roles. When an extensive playbook is needed, it is more useful to run just a part of it as opposed to the entire thing. That is where tags are used.

14. Which protocol does Ansible use to communicate with Linux and Windows?
For Linux, the protocol used is SSH.

For Windows, the protocol used is WinRM.

ansible all -m command -a uptime 
ansible all -m shell -a uptime 
ansible all -a uptime
ansible all -m ping 

23. What is the method to check the inventory vars defined for the host?
This can be done by using the following command:

ansible -m debug -a "var=hostvars['hostname']" localhost

24. Explain Ansible facts
Ansible facts can be thought of as a way for Ansible to get information about a host and store it in variables for easy access. This information stored in predefined variables is available to use in the playbook. To generate facts, Ansible runs the set-up module.

https://www.middlewareinventory.com/blog/ansible-ad-hoc-commands/
