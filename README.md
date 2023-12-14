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
install_mongodb_version: "7.0"
install_mongodb_distribution_release: "{{ ansible_distribution_release | lower }}"
install_mongodb_architecture: "{{ ansible_architecture | lower }}"

install_mongodb_db_user: "mongodb"
install_mongodb_db_group: "mongodb"

install_mongodb_db_path: "/var/lib/mongodb"
install_mongodb_log_path: "/var/log/mongodb"
install_mongodb_log_file: "{{ install_mongodb_log_path }}/mongod.log"
install_mongodb_ssl_path: "/etc/mongodb/ssl"

install_mongodb_bind: "0.0.0.0"
install_mongodb_port: 27017

install_mongodb_ssl: true
install_mongodb_ssl_cert: "{{ install_mongodb_ssl_path }}/my-mongodb-cluster.domain.tld/my-mongodb-cluster.domain.tld.pem.crt"
install_mongodb_ssl_key: "{{ install_mongodb_ssl_path }}/my-mongodb-cluster.domain.tld/my-mongodb-cluster.domain.tld.pem.key"
install_mongodb_ssl_pem_key_file: "/etc/mongodb-pemKeyFile.pem"
install_mongodb_ssl_client_auth: true
install_mongodb_ssl_ca: "{{ install_mongodb_ssl_path }}/my-mongodb-cluster.domain.tld/ca-chain.pem.crt"
install_mongodb_ssl_ca_file: "/etc/mongodb-ca.pem"

install_mongodb_admin_login: "admin"
install_mongodb_admin_password: "admin"

```

The best way is to modify these vars by copy the ./default/main.yml file into the ./vars and edit with your personnals requirements.

You can set vars in the template model in Ansible AWX / Tower or just surchage them during the playbook call.

In order to surchage vars, you have multiples possibilities but for mains cases you have to put vars in your inventory and/or on your AWX / Tower interface.

```YAML
# From inventory
---
inv_install_mongodb_prepare_host_users:
  - login: "mongodb"
    group: "mongodb"

inv_install_mongodb_version: "7.0"
inv_install_mongodb_distribution_release: "{{ ansible_distribution_release | lower }}"
inv_install_mongodb_architecture: "{{ ansible_architecture | lower }}"

inv_install_mongodb_db_user: "mongodb"
inv_install_mongodb_db_group: "mongodb"

inv_install_mongodb_db_path: "/var/lib/mongodb"
inv_install_mongodb_log_path: "/var/log/mongodb"
inv_install_mongodb_log_file: "{{ inv_install_mongodb_log_path }}/mongod.log"
inv_install_mongodb_ssl_path: "/etc/mongodb/ssl"

inv_install_mongodb_bind: "0.0.0.0"
inv_install_mongodb_port: 27017

inv_install_mongodb_ssl: true
inv_install_mongodb_ssl_cert: "{{ inv_install_mongodb_ssl_path }}/my-mongodb-cluster.domain.tld/my-mongodb-cluster.domain.tld.pem.crt"
inv_install_mongodb_ssl_key: "{{ inv_install_mongodb_ssl_path }}/my-mongodb-cluster.domain.tld/my-mongodb-cluster.domain.tld.pem.key"
inv_install_mongodb_ssl_pem_key_file: "{{ inv_install_mongodb_ssl_path }}/my-mongodb-cluster.domain.tld/pemKeyFile.pem"
inv_install_mongodb_ssl_client_auth: true
inv_install_mongodb_ssl_ca: "{{ inv_install_mongodb_ssl_path }}/my-mongodb-cluster.domain.tld/ca-chain.pem.crt"
inv_install_mongodb_ssl_ca_file: "/etc/mongodb-ca.pem"

inv_install_mongodb_admin_login: "admin"
inv_install_mongodb_admin_password: "admin"

```

```YAML
# From AWX / Tower
---

```

### Run

To run this role, you can copy the molecule/default/converge.yml playbook and add it into your playbook:

```YAML
- name: "Include labocbz.install_mongodb"
  tags:
    - "labocbz.install_mongodb"
  vars:
    install_mongodb_version: "{{ inv_install_mongodb_version }}"
    install_mongodb_distribution_release: "{{ inv_install_mongodb_distribution_release }}"
    install_mongodb_architecture: "{{ inv_install_mongodb_architecture }}"
    install_mongodb_db_user: "{{ inv_install_mongodb_db_user }}"
    install_mongodb_db_group: "{{ inv_install_mongodb_db_group }}"
    install_mongodb_db_path: "{{ inv_install_mongodb_db_path }}"
    install_mongodb_log_path: "{{ inv_install_mongodb_log_path }}"
    install_mongodb_log_file: "{{ inv_install_mongodb_log_file }}"
    install_mongodb_ssl_path: "{{ inv_install_mongodb_ssl_path }}"
    install_mongodb_bind: "{{ inv_install_mongodb_bind }}"
    install_mongodb_port: "{{ inv_install_mongodb_port }}"
    install_mongodb_ssl: "{{ inv_install_mongodb_ssl }}"
    install_mongodb_ssl_cert: "{{ inv_install_mongodb_ssl_cert }}"
    install_mongodb_ssl_key: "{{ inv_install_mongodb_ssl_key }}"
    install_mongodb_ssl_pem_key_file: "{{ inv_install_mongodb_ssl_pem_key_file }}"
    install_mongodb_ssl_client_auth: "{{ inv_install_mongodb_ssl_client_auth }}"
    install_mongodb_ssl_ca: "{{ inv_install_mongodb_ssl_ca }}"
    install_mongodb_admin_login: "{{ inv_install_mongodb_admin_login }}"
    install_mongodb_admin_password: "{{ inv_install_mongodb_admin_password }}"
    inv_install_mongodb_ssl_ca_file: "{{ inv_install_mongodb_ssl_ca_file }}"
  ansible.builtin.include_role:
    name: "labocbz.install_mongodb"
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

### 2023-10-06: New CICD, new Images

* New CI/CD scenario name
* Molecule now use remote Docker image by Lord Robin Crombez
* Molecule now use custom Docker image in CI/CD by env vars
* New CICD with needs and optimization

### 2023-11-11: mTLS refacto and secure server

* Server is really secured now
* Refacto on shard (removed)
* Refacto on mTLS

### 2023-12-14: System users

* Role can now use system users and address groups

## Authors

* Lord Robin Crombez

## Sources

* [Ansible role documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
* [Install MongoDB Community Edition on Debian](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-debian/#install-mongodb-community-edition-on-debian)
* [Internal/Membership Authentication](https://www.mongodb.com/docs/manual/core/security-internal-authentication/)
* [TLS/SSL Configuration for Clients](https://www.mongodb.com/docs/v3.0/tutorial/configure-ssl-clients/)
* [Enable Access Control](https://www.mongodb.com/docs/manual/tutorial/enable-authentication/#std-label-enable-access-control)
