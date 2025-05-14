# Ansible Project Template

This is a structured template for organizing Ansible projects following best practices. It is designed to help you quickly get started with managing inventories, playbooks, roles, collections, and testing.

## Project Structure Overview

```
.
├── ansible.cfg               # Main Ansible configuration
├── collections/              # Ansible collections
│   └── requirements.yml     # Collection dependencies
├── inventories/             # Inventory files for different environments
│   ├── production/         # Production environment
│   │   ├── group_vars/    # Group variables for production
│   │   ├── host_vars/     # Host-specific variables for production
│   │   └── hosts.yml      # Production hosts definition
│   └── staging/           # Staging environment
│       ├── group_vars/    # Group variables for staging
│       ├── host_vars/     # Host-specific variables for staging
│       └── hosts.yml      # Staging hosts definition
├── playbooks/              # Playbooks directory
│   ├── site.yml           # Main playbook
│   ├── webserver.yml      # Webserver configuration
│   └── database.yml       # Database configuration
├── roles/                  # Roles directory
│   ├── common/            # Common configuration role
│   ├── webserver/         # Webserver role
│   └── database/          # Database role
├── files/                  # Static files
├── templates/              # Jinja2 templates
└── tests/                  # Test directory
    └── molecule/          # Molecule test configurations
```

## Explanation of Key Components

### ansible.cfg

This is the main configuration file for Ansible. It contains default settings such as:
- Location of inventory files
- SSH configuration
- Callback plugins
- Performance optimizations

### collections/

This directory contains the `requirements.yml` that defines all required Ansible Collections. Collections are bundles of modules, plugins, and roles that extend Ansible's functionality. Install collections with:

```bash
ansible-galaxy collection install -r collections/requirements.yml
```

### inventories/

Contains environment-specific inventories (production, staging, etc.). Each environment has:
- `hosts.yml`: Definition of hosts and groups
- `group_vars/`: Variables for groups of hosts
- `host_vars/`: Host-specific variables

### playbooks/

Contains all playbooks for your automation needs:
- `site.yml`: The main playbook that imports other playbooks
- `setup.yml`: Initial setup and configuration
- `deploy.yml`: Deployment related tasks

Add more specific playbooks based on your project requirements.

### roles/

Contains reusable roles with a standardized structure:
- `common/`: Base configuration for all targets
- `setup/`: Initial setup and configuration tasks
- `deploy/`: Deployment and maintenance tasks

Each role has the following structure:
- `defaults/`: Default variables
- `files/`: Static files
- `handlers/`: Event handlers
- `meta/`: Role metadata and dependencies
- `tasks/`: Main tasks of the role
- `templates/`: Jinja2 templates
- `vars/`: Role-specific variables

### files/ & templates/

- `files/`: Contains static files to be copied to servers
- `templates/`: Contains Jinja2 templates used in playbooks and roles

### tests/

Contains Molecule test configurations for testing roles and playbooks in isolated environments (e.g., Docker containers):
- Test scenarios
- Verifier configuration
- Test playbooks

## Getting Started

1. **Configure your inventory:**
   ```bash
   # Copy example files
   cp -r inventories/staging inventories/production
   # Edit hosts and variables
   vim inventories/production/hosts.yml
   ```

2. **Install collections:**
   ```bash
   ansible-galaxy collection install -r collections/requirements.yml
   ```

3. **Develop roles:**
   ```bash
   # Create a new role
   ansible-galaxy role init roles/new-role
   ```

4. **Test your roles:**
   ```bash
   cd roles/new-role
   molecule test
   ```

5. **Run playbooks:**
   ```bash
   # Test in staging first
   ansible-playbook playbooks/site.yml -i inventories/staging/hosts.yml
   
   # Then production
   ansible-playbook playbooks/site.yml -i inventories/production/hosts.yml
   ```

## Best Practices

1. **Version Control:**
   - Use Git for version control
   - Add `.retry` and `*.pyc` files to `.gitignore`
   - Use branches for major changes

2. **Security:**
   - Use Ansible Vault for sensitive data
   - Separate inventories per environment
   - Regular inventory backups

3. **Testing:**
   - Test roles with Molecule
   - Use `--check` mode for dry-runs
   - Test in staging first

4. **Maintenance:**
   - Keep collections up-to-date
   - Document changes
   - Regular review and refactoring

---

This template provides a solid foundation for scalable and maintainable Ansible automation. Customize it according to your needs.

Happy automating!