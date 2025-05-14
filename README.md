# Ansible Project Template

This repository provides a structured template for organizing Ansible projects. It is designed to help you get started quickly with best practices for managing inventories, playbooks, roles, collections, and testing.

## Project Structure Overview

```
.
├── ansible.example.cfg
├── collections
│   └── requirements.yml
├── example
│   ├── deployment.yml
│   └── service.yml
├── inventory
│   └── sample
│       ├── group_vars
│       │   ├── all.yml
│       │   └── custom.yml
│       └── hosts.ini
├── molecule
│   └── default
│       ├── molecule.yml
│       └── prepare.yml
├── playbook.yml
├── README.md
└── roles
    └── example_role
        ├── defaults
        ├── meta
        └── tasks
```

## Explanation of Key Components

### ansible.example.cfg

This is the main Ansible configuration file. It sets default options such as the inventory file location, disabling host key checking, and disabling retry files. You can customize this file to suit your environment.

### collections/requirements.yml

This file lists the Ansible Collections your project depends on. Collections are bundles of modules, plugins, and roles that extend Ansible’s functionality. Use this file with the command:

```bash
ansible-galaxy collection install -r collections/requirements.yml
```

to install required collections.

### example/

This directory contains example playbooks such as `deployment.yml` and `service.yml`. These playbooks define tasks and workflows to be executed on your managed hosts.

### inventory/

The inventory directory holds your host and group definitions.

- `hosts.ini` is an INI-format inventory file listing your hosts and groups.
- `group_vars/` contains YAML files defining variables for groups of hosts. For example, `all.yml` applies to all hosts, while `custom.yml` can be for a specific group.

### molecule/

This directory is for Molecule testing, which allows you to test your roles and playbooks in isolated environments (e.g., Docker containers).

- `molecule.yml` defines the test scenarios and platforms.
- `prepare.yml` is a playbook to set up the test environment before running tests.

### playbook.yml

A simple example playbook that runs a ping module against all hosts in the inventory. This is a good starting point to verify connectivity.

### roles/

Roles are reusable, modular units of Ansible content. Each role has a standardized directory structure:

- `defaults/` contains default variables for the role.
- `meta/` contains metadata such as role dependencies.
- `tasks/` contains the main list of tasks to be executed by the role.

Using roles helps keep your playbooks clean and promotes reuse.

## Getting Started

1. **Configure your inventory:** Edit `inventory/sample/hosts.ini` to list your hosts and groups.
2. **Define variables:** Add group or host variables in `inventory/sample/group_vars/`.
3. **Write playbooks:** Use the `example/` directory or create new playbooks to automate tasks.
4. **Create roles:** Develop roles under `roles/` to organize complex configurations.
5. **Run playbooks:** Execute your playbooks with:

```bash
ansible-playbook playbook.yml -i inventory/sample/hosts.ini
```

6. **Test roles:** Use Molecule to test your roles locally before deploying.

## Additional Tips

- Keep your `ansible.example.cfg` updated with environment-specific settings.
- Use collections to leverage community or custom modules.
- Structure your roles logically to maximize reuse.
- Use Molecule for continuous integration and testing of your Ansible content.

---

This template is a solid foundation for building scalable and maintainable Ansible automation projects. Feel free to customize it according to your needs.

Happy automating!