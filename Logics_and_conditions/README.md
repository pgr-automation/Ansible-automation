# Ansible Conditional Execution Examples

Ansible allows you to control task execution based on conditions using logical operators like AND, OR, and NOT IN. Here are some examples of how to use these conditions effectively:

## Using AND Condition

If you want a task to run only when all conditions are true, you can use the `AND` operator.

```yaml
tasks:
  - name: Example with AND condition
    debug:
      msg: "All conditions met!"
    when:
      - ansible_os_family == 'Debian'
      - ansible_distribution_version == '10'
```

- using and to combine conditions:
```yaml
tasks:
  - name: Example with AND condition (using `and`)
    debug:
      msg: "All conditions met!"
    when: ansible_os_family == 'Debian' and ansible_distribution_version == '10'
```

## Using OR Condition
- To run a task if any condition is true, use the OR operator.

```yaml
tasks:
  - name: Example with OR condition
    debug:
      msg: "One of the conditions is met!"
    when: ansible_os_family == 'Debian' or ansible_os_family == 'RedHat'
```
## Combining AND and OR
- Combine both AND and OR conditions for complex logic, ensuring to use parentheses for grouping.
```yaml
tasks:
  - name: Example with AND and OR conditions
    debug:
      msg: "Complex condition met!"
    when: (ansible_os_family == 'Debian' and ansible_distribution_version == '10') or (ansible_os_family == 'RedHat' and ansible_distribution_version == '8')
```

## Using NOT IN Condition
- You can use not in to check if a value is not present in a list or string.
```yaml
tasks:
  - name: Check if a package is not installed
    debug:
      msg: "The package is not installed."
    when: "'nginx' not in ansible_facts.packages"
```
