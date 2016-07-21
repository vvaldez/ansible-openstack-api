# ansible-openstack-api

## Ansible Version
NOTE: Tested with Ansible 1.9.4 but should work with 2.x, though many of these tasks could be easily performed via the 2.x **os_** modules instead.

## Demo
In-depth screencast demonstrating this playbook: https://youtu.be/HV9MN3tNzvg

## About
This playbook uses Ansible URI module to communicate with OpenStack APIs using JSON.

This playbook grabs an authentication token from the OpenStack Identity service and reuses that through several tasks as admin. It creates a project and user based on defined variables then revokes the token and authenticates as the new user to complete the remainder of the tasks. For a project I was working on we were stuck using Ansible 1.9.x so could not take advantage of some of the new 2.x modules. However, this playbook runs considerably faster than using shell/command modules or a bash script with equivalent CLI command.

Some of the advantages of this approach over OpenStack CLI commands or even what modules do work is that authentication does not need to be provided on every single CLI invocation. Reusing then revoking the token is much faster so as the number of tasks invoked increases so does the efficiency of this approach. The API also returns native JSON which makes accessing object data a snap, rather than using a shell or command module and painstakingly trying to awk/grep or otherwise get at the data you need.

I plan on enhancing this with additional actions and possibly converting it into a role but want to evaluate options and effects of Ansible 2.x.

## Related
This playbook is only a small subset of a larger set of work which involves going on to create instances and a dynamic inventory and installing OpenShift. For more details see https://github.com/rhtconsulting/rhc-ose/tree/openshift-enterprise-3/rhc-ose-ansible
