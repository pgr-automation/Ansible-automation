# Ansible Playbook
An Ansible playbook is a YAML file that defines a series of tasks to be executed on one or more hosts. Playbooks are the primary means of defining automation with Ansible. They can manage systems, deploy applications, and orchestrate complex workflows. Playbooks consist of one or more "plays," which map a group of hosts to a set of roles and tasks. Each task describes a specific action to perform, such as installing a package, copying files, or starting a service.

## Commands

1. Run a Playbook:
```bash
ansible-playbook -i inventory_file playbook.yml
```
2. Check Mode (dry run):
```bash
ansible-playbook -i inventory_file playbook.yml --check
```
3. Limit Execution to Specific Hosts:
```bash
ansible-playbook -i inventory_file playbook.yml --limit hostname
```
4. Specify a Different Vault Password File:
```bash
ansible-playbook -i inventory_file playbook.yml --vault-password-file vault_pass.txt
```
