bika.ansible-playbook
=====================

Configure and manage multiple load-balanced Plone zeoclusters behind 
nginx and varnish.

1) Clone the repository

    git clone https://github.com/bikalabs/bika.ansible-playbook.git
    cd bika.ansible-playbook

2) do the little submodule dance

    git submodule update --init ansible.plone_server
    
> This checks out ansible.plone_server from a branch which disambiguates
  between supervisor/cron instances on the same server.  When this
  gets implemented into plone/ansible.plone_server, the behaviour
  we have here might change a little.

3) Create ansible hosts inventory.  I use ./hosts.cfg, it's in .gitignore.

4) Create host_vars for each instance you need to create.  Copy
   host_vars/example to /host_vars/{{ host }}. edit the
   file, and save it.

   The name used for the host in the inventory must match up with the
   filename in host_vars/ exactly. This same identifier is used when
   creating Plone instances, supervisor configurations, nginx and varnish
   configurations, and a few others too.  I just refer to it as "host".

The first time you access a server, you need to install system dependencies:

    ansible-playbook -i hosts.cfg --limit=host1,host2 tasks/setup-server.yml 

After that, you can add new Plone instances as you like.  Each new Plone
instance will consist of:

    - Configuration in /etc/nginx/sites-enabled/<host>.conf
    - Configuration in /etc/varnish/sites/<host>.vcl
    - Configuration in /etc/supervisor/conf.d/<host>.conf
    - Plone instance in /usr/local/plone-x.y/<host>
    - Plone storage in /var/local/plone-x.y/<host>

To configure each instance run:

    ansible-playbook -i hosts.cfg --limit=host1,host2 tasks/configure.yml

To stop, start, or restart, use these:

    ansible-playbook -i hosts.cfg --limit=host1,host2 tasks/stop.yml
    ansible-playbook -i hosts.cfg --limit=host1,host2 tasks/start.yml
    ansible-playbook -i hosts.cfg --limit=host1,host2 tasks/restart-clients.yml

A playbook for updating all sources, running buildout, and restarting all
zeoclients:

    ansible-playbook -i hosts.cfg --limit=host1,host2 tasks/update.yml
