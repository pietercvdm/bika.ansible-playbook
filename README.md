bika.ansible-playbook
=====================

Configures multiple load-balanced Plone zeoclusters behind nginx and varnish.
 
1) clone the repository

2) copy hosts/example-vars.yml to /hosts/{{ instance_identifier }}-vars.yml,
   and edit it.

3) Setup some servers:

    bin/configure {{ instance_identifier }}"

Additional parameters are passed straight to ansible-playbook.

The bin/configure contains the ansible-playbook command, and it assumes that 
ansible-playbook is in the path.
