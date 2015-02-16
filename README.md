bika.ansible-playbook
=====================

Configure and manage multiple load-balanced Plone zeoclusters behind 
nginx and varnish.
 
1) Clone the repository

    git clone https://github.com/bikalabs/bika.ansible-playbook.git
    cd bika.ansible-playbook

2) Create ansible hosts file at ./hosts.cfg.

3) Copy host_vars/example to /host_vars/{{ instance_id }}.
   edit the file, and save it.

4) Setup some servers:

  bin/bapl setup-server server_host    # one-time deps, etc
  bin/bapl configure example_instance  # plone instance
  bin/bapl update example_instance     # update src/
  bin/bapl stop example_instance       # supervisor command
  bin/bapl start example_instance      # supervisor command
  
Additional parameters are passed straight to ansible-playbook,
so you can use --check and --diff etc, and you can also use "all"
for the instance, and add your own --limit= arguments.
