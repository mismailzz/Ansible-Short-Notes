# Ansible-Short-Notes
The content is taken from the book "Ansible for DevOps - Server and configuration management for humans" by Jeff Geerling. Furthermore, this repository also contain the ad-hoc commands and playbooks from personal experience.

### Table of Contents  

[Configuration](#config)  

[Parallel Execution](#fork)

[Privilege Escalation](#pescalation)

[Limit Servers Selection](#lselection)
<a name="config"/>
## Configuration
```
export ANSIBLE_INVENTORY=/etc/ansible/hosts
ANSIBLE_HOST_KEY_CHECKING=False
```
<a name="fork"/>

## Parallelism

```
By default, Ansible will run your commands in parallel, using multiple process forks, so the command will complete more quickly. 
$ ansible multi -a "hostname" -f 1
```
<a name="pescalation"/>

## Privilege Escalation

```
The option (alias for -become) tells Ansible to run the command with -b - become (basically, run commands with ‘sudo’. This will work fine with our Vagrant VMs, but if you’re running commands against a server where your user account requires a password for privilege escalation, you should also pass in (alias for -pass), so you can enter your password -K --ask-become when Ansible needs it.
```
<a name="lselection"/>

## Limit Inventory or Specific server

```
$ ansible app -b -a "service ntpd restart" --limit "192.168.60.4"

In this command, we used the argument to limit the command to a specific --limit host in the specified group. will match either an exact string or a regular --limit expression (prefixed with ~).

Limit hosts with a simple pattern (asterisk is a wildcard).
$ ansible app -b -a "service ntpd restart" --limit "*.4"

# Limit hosts with a regular expression (prefix with a tilde).
$ ansible app -b -a "service ntpd restart" --limit ~".*\.4"
```


