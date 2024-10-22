# Ansible Roles: Complete Guide

Ansible roles are a way to organize your automation tasks into reusable, modular components. This guide will walk you through the basics of creating, using, and managing roles in Ansible.

## What is an Ansible Role?

An Ansible role is a way to break down playbooks into smaller, reusable components. Each role is responsible for managing a particular piece of configuration, such as installing a service or configuring a specific aspect of a system.

Roles allow for better organization, easier reuse, and more modularity in complex playbooks.

## Role Directory Structure

A typical Ansible role has the following directory structure:

```bash
roles/
  └── <role_name>/
      ├── tasks/
      │   └── main.yml
      ├── handlers/
      │   └── main.yml
      ├── files/
      ├── templates/
      ├── vars/
      │   └── main.yml
      ├── defaults/
      │   └── main.yml
      ├── meta/
      │   └── main.yml
      └── tests/
          ├── inventory
          └── test.yml
```

### Directory Descriptions:

- tasks/: Contains the main list of tasks to be executed by the role. Tasks are defined in YAML format and main.yml is the entry point.
- handlers/: Defines handlers that are triggered by notify statements from tasks (e.g., restarting a service).
- files/: Stores static files that you want to be copied to the target machines.
- templates/: Contains Jinja2 templates, which are dynamically generated files based on variables.
- vars/: Stores role-specific variables.
- defaults/: Contains default variables that can be overridden by the user.
- meta/: Provides metadata about the role (e.g., dependencies).
- tests/: Includes tests for the role to ensure functionality.

### Create the Role Directory

You can initialize the structure using Ansible Galaxy:

```bash
ansible-galaxy init nginx
```
