bika.ansible-playbook
=====================

Configure and manage multiple load-balanced Plone zeoclusters behind 
nginx and varnish.
 
1) Clone the repository

    git clone https://github.com/bikalabs/bika.ansible-playbook.git
    cd bika.ansible-playbook

2) Create ansible hosts file at ./hosts.cfg.

> The bin/bapl script assumes this.  Humor it.  Or add a blank hosts.cfg file, and specify your own using the normal "-i" syntax when calling /bin/bapl (bapl passes all extra arguments directly to ansible-playbook).

3) Copy host_vars/example to /host_vars/{{ instance_id }}.
   edit the file, and save it.

> instance_id is used for the following: plone_instance_name, plone_site_id, supervisor_instance_name, plone_cron_prefix, the nginx and varnish configurations, and the supervisor configuration.  Probably a couple of others.

4) Setup some servers:

    bin/bapl setup-server server_host    # one-time deps, etc
    bin/bapl configure example_instance  # plone instance
    bin/bapl update example_instance     # update src/
    bin/bapl stop example_instance       # supervisor command
    bin/bapl start example_instance      # supervisor command

Additional parameters are passed straight to ansible-playbook,
so you can use --check and --diff etc.

You can also use "all" for the instance, which requires confirmation.

If you do this, you can then and add your own --limit= arguments to
specify arbitrary lists of hosts to apply.  To (re-)configure Plone
sites for a set of hosts:

    bin/bapl configure all --limit server1,server2,server3
