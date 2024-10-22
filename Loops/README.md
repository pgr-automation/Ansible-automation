# Ansible Loops

In Ansible, loops are used to repeat tasks multiple times with different variables or conditions. This document explains different ways to implement loops in Ansible based on specific use cases.

## 1. Basic Looping

You can use the `loop` keyword to iterate over a list of items. This is the most basic form of looping in Ansible.

### Example: Loop through a list of users to create them
```yaml
- name: Create multiple users
  user:
    name: "{{ item }}"
    state: present
  loop:
    - alice
    - bob
    - charlie
```
## 2. Looping over Dictionaries (key-value pairs)
When you have a dictionary and want to loop through both keys and values, you can use with_dict or loop.
Example: Create users with specific attributes
```yaml
- name: Create users with specific attributes
  user:
    name: "{{ item.key }}"
    uid: "{{ item.value.uid }}"
    shell: "{{ item.value.shell }}"
  loop:
    - { key: 'alice', value: { uid: 1001, shell: '/bin/bash' } }
    - { key: 'bob', value: { uid: 1002, shell: '/bin/zsh' } }
```
## 3. Loop with Range

You can use a loop to iterate over a range of numbers using the range filter.
Example: Create a series of files
```yaml
- name: Create a series of files
  file:
    path: "/tmp/file{{ item }}"
    state: touch
  loop: "{{ range(1, 6) | list }}"
```
* - This will create files /tmp/file1, /tmp/file2, ..., /tmp/file5.

## 4. Loop with Nested Data

Ansible supports nested loops using with_nested or loop with two lists.
Example: Nested loop for combining lists
```yaml
- name: Install multiple versions of multiple software
  command: "{{ item.0 }} --version {{ item.1 }}"
  loop:
    - [ 'python', 'nodejs', 'ruby' ]
    - [ '2.7', '3.9', '14.17' ]
```

## 5. Loop with Index

If you need access to the index (the position) of the items in the loop, you can use loop.index or loop.index0.
Example: Loop with index
```yaml
- name: Print index and value
  debug:
    msg: "Index {{ loop.index }}: {{ item }}"
  loop:
    - apple
    - banana
    - cherry
```
## 6. Loop Control with until

Ansible also allows looping with retries using the until parameter in combination with retries and delay.
Example: Retry a task until a condition is met

```yaml
- name: Wait for service to be available
  shell: curl -s http://localhost:8080
  register: result
  until: result.stdout.find("Welcome") != -1
  retries: 5
  delay: 10
```
## 7. Loop with Conditional Execution

You can use a loop in combination with conditions to control when certain iterations are executed.
Example: Conditional looping
```yaml
- name: Add users only if the group exists
  user:
    name: "{{ item }}"
    state: present
  loop:
    - alice
    - bob
  when: ansible_facts['ansible_distribution'] == 'Ubuntu'
```


