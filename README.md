# Ansible role: labocbz.install_mongodb

![Licence Status](https://img.shields.io/badge/licence-MIT-brightgreen)
![CI Status](https://img.shields.io/badge/CI-success-brightgreen)
![Testing Method](https://img.shields.io/badge/Testing%20Method-Ansible%20Molecule-blueviolet)
![Testing Driver](https://img.shields.io/badge/Testing%20Driver-docker-blueviolet)
![Language Status](https://img.shields.io/badge/language-Ansible-red)
![Compagny](https://img.shields.io/badge/Compagny-Labo--CBZ-blue)
![Author](https://img.shields.io/badge/Author-Lord%20Robin%20Crombez-blue)

## Description

![Tag: Ansible](https://img.shields.io/badge/Tech-Ansible-orange)
![Tag: Debian](https://img.shields.io/badge/Tech-Debian-orange)
![Tag: MongoDB](https://img.shields.io/badge/Tech-MongoDB-orange)
![Tag: SSL/TLS](https://img.shields.io/badge/Tech-SSL%2FTLS-orange)

An Ansible role to install and configure MongoDB on your host.

The Ansible role offers seamless deployment and configuration of MongoDB, tailored to your specific version requirements. This role streamlines the process of setting up MongoDB while providing a range of customizable options to enhance security and communication.

With the ability to define the MongoDB version this role ensures you have the latest features and improvements at your fingertips. The installation is adapted to your system's architecture, intelligently determined by factors such as the distribution release and architecture of your machine.

Enabling robust security measures, this role facilitates the setup of SSL and mTLS encryption. Leveraging SSL certificates located in designated paths, you can be confident in securing your MongoDB deployment. Mutual authentication is also supported for enhanced verification, ensuring secure communication across your network.

Additionally, the role introduces an administrative layer of protection. A super administrator, configured with the credentials "admin" and "admin," empowers you to manage and oversee your MongoDB deployment with utmost authority and control. The role prioritizes security, empowering you to confidently manage your MongoDB database environment.

It's important to note that this role currently does not support cluster mode configuration. However, rest assured that this feature is actively being developed and will soon be seamlessly integrated into the role's capabilities.

In summary, this Ansible role is your trusted companion for effortlessly setting up, securing, and administering MongoDB. Experience a smooth and secure deployment process, confident in the knowledge that you're equipped with the latest version, SSL encryption, and a dedicated super administrator. Elevate your MongoDB experience with this role, simplifying your management tasks and bolstering your database's integrity.

## Folder structure

By default Ansible will look in each directory within a role for a main.yml file for relevant content (also man.yml and main):

```PYTHON
.
├── README.md  # Contains an overview of the role and its purpose.
├── defaults
│   ├── main.yml  # Contains default variables for the role that can be overridden by users.
│   └── README.md  # Contains documentation for the default variables.
├── files
│   └── README.md  # Contains documentation for the files in the directory.
├── handlers
│   ├── main.yml  # Contains handlers that can be called by tasks within the role.
│   └── README.md  # Contains documentation for the handlers.
├── meta
│   ├── main.yml  # Contains metadata about the role, including dependencies and supported platforms.
│   └── README.md  # Contains documentation for the role metadata.
├── tasks
│   ├── main.yml  # Contains tasks to be executed by the role on the managed nodes.
│   └── README.md  # Contains documentation for the tasks.
├── templates
│   └── README.md  # Contains documentation for the templates.
└── vars
    ├── main.yml  # Contains variables that are specific to the role and are not meant to be overridden.
    └── README.md  # Contains documentation for the role variables.
```

## Tests and simulations

### Basics

You have to run multiples tests. *tests with an # are mandatory*

```MARKDOWN
# lint
# syntax
# converge
# idempotence
# verify
side_effect
```

Executing theses test in this order is called a "scenario" and Molecule can handle them.

Molecule use Ansible and pre configured playbook to create containers, prepare them, converge (run the role) and verify its execution.
You can manage multiples scenario with multiples tests in order to get a 100% code coverage.

This role contains a ./tests folder. In this folder you can use the inventory or the tower folder to create a simualtion of a real inventory and a real AWX / Tower job execution.

### Command reminder

```SHELL
# Check your YAML syntax
yamllint -c ./.yamllint .

# Check your Ansible syntax and code security
ansible-lint --config=./.ansible-lint .

# Execute and test your role
molecule lint
molecule create
molecule list
molecule converge
molecule verify
molecule destroy

# Execute all previous task in one single command
molecule test
```

## Installation

To install this role, just copy/import this role or raw file into your fresh playbook repository or call it with the "include_role/import_role" module.

## Usage

### Vars

Some vars a required to run this role:

```YAML
---
your defaults vars here
```

The best way is to modify these vars by copy the ./default/main.yml file into the ./vars and edit with your personnals requirements.

You can set vars in the template model in Ansible AWX / Tower or just surchage them during the playbook call.

In order to surchage vars, you have multiples possibilities but for mains cases you have to put vars in your inventory and/or on your AWX / Tower interface.

```YAML
# From inventory
---
all vars from to put/from your inventory
```

```YAML
# From AWX / Tower
---
all vars from to put/from AWX / Tower
```

### Run

To run this role, you can copy the molecule/default/converge.yml playbook and add it into your playbook:

```YAML
---
your converge.yml file here
```

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-08-18: First Init

* First init of this role with the bootstrap_role playbook by Lord Robin Crombez
* Role install MongoDB
* Repository added from based vars distribution
* Security module enabled and admin login/password setted
* SSL/TLS / mTLS setted
* No cluster for now, because no working tutorial founded for now

## Authors

* Lord Robin Crombez

## Sources

* [Ansible role documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
* [Install MongoDB Community Edition on Debian](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-debian/#install-mongodb-community-edition-on-debian)
* [Internal/Membership Authentication](https://www.mongodb.com/docs/manual/core/security-internal-authentication/)
* [TLS/SSL Configuration for Clients](https://www.mongodb.com/docs/v3.0/tutorial/configure-ssl-clients/)
* [Enable Access Control](https://www.mongodb.com/docs/manual/tutorial/enable-authentication/#std-label-enable-access-control)
