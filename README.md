Enix/logstash
=================

A role for deploying and configuring [Logstash](https://www.elastic.co/products/logstash) on unix hosts using [Ansible](http://www.ansible.com/).


Requirements
------------

Supported targets:

- Debian 8 "Jessie"
- ...


Role Variables
--------------

This roles comes preloaded with almost every available default. You can override each one in your hosts/group vars, in your inventory, or in your play. See the annotated defaults in `defaults/main.yml` for help in configuration. All provided variables start with `logstash_`.

- `logstash_plugins: []` - list of logstash plugins to install.

Dependencies
------------

Ansible roles, can be pulled by ansible-galaxy or by hand in roles/

- `Enix/elastic-repo`: https://gitlab.enix.org/ansible/ansible-elastic-repo.git.


Usage
-----

Clone this repo into your roles directory:

    $ git clone https://gitlab.enix.org/ansible/ansible-logstash.git roles/logstash

Or use Ansible galaxy requirements.yml

And add it to your play's roles:

    - hosts: servers
      roles:
        - role: logstash
          logstash_plugins:
            - { plugin_name: "logstash-output-lumberjack" }


You can also use the role as a playbook. You will be asked which hosts to provision, and you can further configure the play by using `--extra-vars`.

    $ ansible-playbook -i inventory --extra-vars='{...}' main.yml


Still to do
-----------

- Add depends on java role for java8 installation as separate usage
- Add RedHat compatibility
- Must find a way to not install plugins each time (list output check)

Changelog
---------

### 0.1

Initial version.

License
-------

BSD

Author Information
------------------

Laurent.CORBES <laurent.corbes@enix.fr> - http://www.enix.fr
