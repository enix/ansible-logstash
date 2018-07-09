eNiXHosting.logstash
=================

A role for deploying and configuring [Logstash](https://www.elastic.co/products/logstash) on unix hosts using [Ansible](http://www.ansible.com/).


Requirements
------------

Supported targets:

- Debian 8 "Jessie"


Role Variables
--------------

This roles comes preloaded with almost every available default. You can override each one in your hosts/group vars, in your inventory, or in your play. See the annotated defaults in `defaults/main.yml` for help in configuration. All provided variables start with `logstash_`.

- `logstash_plugins: []` - list of logstash plugins to install.
- `logstash_options: ""` - block of options to append to logstash.yml.
- `logstash_longstartupworkaround: false` - enable the long java startup workaround (Change the entropy source to urandom)
- `logstash_bindprivileged: false` - allow logstash to listen on privileged ports (needed for syslog reception on ports 514)
- `logstash_configuration: ""` - directory with configuration stored, copied into `/etc/logstash/conf.d/` (must have a trailing /).
- `logstash_configurationtemplates: ""` - list of files to template and copy to `/etc/logstash/conf.d/` (Apllied after copying the base configuration).

Dependencies
------------

Ansible roles, can be pulled by ansible-galaxy or by hand in roles/

- `eNiXHosting.elastic_repo`: https://galaxy.ansible.com/eNiXHosting/elastic_repo/.


Usage
-----

Clone this repo into your roles directory:

    $ git clone https://gitlab.enix.org/ansible/ansible-logstash.git roles/logstash

Or use Ansible galaxy requirements.yml

    # eNiXHosting.logstash galaxy role
    - src: eNiXHosting.logstash
      name: logstash

And add it to your play's roles:

    - hosts: servers
      roles:
        - role: logstash
          logstash_plugins:
            - { plugin_name: "logstash-output-lumberjack" }
          logstash_options: |
            queue.type: persisted
            path.queue: /var/lib/logstash/queue
            queue.max_bytes: 4gb
          logstash_longstartupworkaround: true
          logstash_bindprivileged: true
          logstash_configuration: "files/logstash.d/"


You can also use the role as a playbook. You will be asked which hosts to provision, and you can further configure the play by using `--extra-vars`.

    $ ansible-playbook -i inventory --extra-vars='{...}' main.yml


Still to do
-----------

- Add depends on Java role for java8 installation as separate usage
- Move out Java binary privileged flag into dedicated Java role
- Add RedHat compatibility
- Must find a way to not install plugins each time (list output check)
- When Ansible 2.3 available widely, use logstash_plugins module
- Use synchronize instead of copy for configuration to support deletion of files
- Change variables to logstash__

Changelog
---------

### 1.0

Initial version.

License
-------

GPLv2

Author Information
------------------

Laurent.CORBES <laurent.corbes@enix.fr> - http://www.enix.fr
