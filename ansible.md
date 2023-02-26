ANSIBLE
:ansible:

# Contents

- [Configure Your Own Host](#Configure Your Own Host)
- [Glossary](#Glossary)
- [References](#References)
- [Ad-hoc Commands](#Ad-hoc Commands)
- [Inventory](#Inventory)
- [Variables](#Variables)
- [Playbooks](#Playbooks)
- [Roles](#Roles)

# Configure Your Own Host

[Using Ansible to set up a workstation - Fedora Magazine](https://fedoramagazine.org/using-ansible-setup-workstation/)

[Ansible Archlinux - Automated arch linux desktop environment - (ansible-archlinux)](https://opensourcelibs.com/lib/ansible-archlinux)

# Glossary

Important terms used in Ansible:
    * Ansible server: The machine where Ansible is installed and from which all tasks and playbooks will be ran
    * Module: Basically, a module is a command or set of similar Ansible commands meant to be executed on the client-side
    * Task: A task is a section that consists of a single procedure to be completed
    * Role: A way of organizing tasks and related files to be later called in a playbook
    * Fact: Information fetched from the client system from the global variables with the gather-facts operation
    * Inventory: File containing data about the ansible client servers. Defined in later examples as hosts file
    * Play: Execution of a playbook
    * Handler: Task which is called only if a notifier is present
    * Notifier: Section attributed to a task which calls a handler if the output is changed
    * Tag: Name set to a task which can be used later on to issue just that specific task or group of tasks.


# References

    * [YAML Syntax — Ansible Documentation](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html)
    * [Index of all Modules — Ansible Documentation](https://docs.ansible.com/ansible/latest/collections/index_module.html)
    * [Ansible Tutorial for Beginners: Playbook & Examples](https://spacelift.io/blog/ansible-tutorial)
    * [Ansible Tutorial for Beginners: Playbook, Commands & Example](https://www.guru99.com/ansible-tutorial.html)

# Ad-hoc Commands

`ansible -i [host-pattern] -m [module] -a “[module options]”`
    * `-i` inventory host path or comma separated host list
    * `-m` the module to run
    * `-a` the list of arguments required by the module
    * `--limit <hosts>` limit the command to some hosts
    * ex: `ansible -i hosts all -m ping`
    * ex: `ansible -i hosts all -m yum -a 'name=ncdu state=present'` install ncdu package to all hosts



# Inventory

The list of hosts files for the inventory can be defined in a file. Add the list to your ansible.cfg

The hosts file then will have the definitions of those hosts.

`ansible-inventory --list` test inventory

# Variables

You can define variables at different levels.

At playbook level you would define it at the top level

# Playbooks

Playbooks can consist of multiple tasks. Or you can call roles from them.

```
---
- name: My Playbook
  hosts: all
  vars:
      user: tzvi
      package: ufw
      state: latest
  tasks:
  - name: add the user {{ user }}
    ansible.builtin.user:
      name: "{{ user }}"
  - name: Install the {{ state }} of package {{ package }}
    apt:
      name: "{{ package }}"
      state: "{{ state }}"
  roles:
    - { role: <role1>, tags: lalala }
    - { role: <role2>, tags: beep }
```


    * `ansible-playbook -i hosts p4.yml --check` dry-run the playbook
    * `ansible-playbook -i hosts p4.yml -k` run p4 playbook with password authentication

# Roles

Roles are stored in separate directories and have a particular dir structure.

`ansible-galaxy init <role-name>` An easy way to initiate the role directory and its contents

`-- role1
    |-- defaults
    |   `-- main.yml
    |-- handlers
    |   `-- main.yml
    |-- meta
    |   `-- main.yml
    |-- README.md
    |-- tasks
    |   `-- main.yml
    |-- tests
    |   |-- inventory
    |   `-- test.yml
    `-- vars
        `-- main.yml

    * `defaults/` contains default vars that are to be used along with the playbook
    * `handlers/` stores handlers
    * `meta/` contains info about the author and role dependencies
    * `tasks/` tasks go here - it contains the `main.yml` - the main yaml file for the role
    * `tests/` contains tests
    * `vars/` contains the yaml file in which all the variables used by the role are defined
    * `templates/` and `files/` if you have those, will contain the jinja templates and files used by the role
