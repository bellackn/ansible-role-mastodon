bellackn.mastodon
=================

This role deploys a Mastodon instance running in Docker.

Role Variables
--------------

    mastodon_version: v3.3.0

The version of Mastodon that will be used.

    mastodon_whitelist_mode: no

Whether you want to run the Mastodon instance in whitelist mode. Check this [blog post][1] for more information

    mastodon_install_dir: /opt/mastodon

Directory in which Mastodon will be installed.

    mastodon_nginx: no

If activated, the role will set up an nginx instance as reverse proxy for Mastodon.
> *WARNING:* This is not yet tested since my setup is different. 

    mastodon_migrate_database: yes
    mastodon_precompile_assets: yes

This will perform a database migration and precompile the assets. Probably you should only have to run this when you 
initially set up your instance, after that you can deactivate this.

    mastodon_domain:

Domain under which your instance can be accessed.

    mastodon_db_pass:

Password for the Postgres database.

    mastodon_smtp:
      server:
      port:
      login:
      password:
      from_address:

SMTP options for your instance.

Dependencies
------------

You need to have the following installed on your controlhost:
* Ansible role `geerlingguy.pip` (version `2.0.0`)
* Ansible role `geerlingguy.docker` (version `3.0.0`)

Example Playbook
----------------

    ---
    - name: Configure Mastodon
      hosts: mastodon
      become: yes
      gather_facts: yes
    
      vars:
        mastodon_domain: example.com
        mastodon_db_pass: db-password
        mastodon_smtp:
          server: your-smtp-server
          port: 587
          login: your-login
          password: smtp-password
          from_address: mastodon@your-domain

        # Comment these out when starting from scratch
        mastodon_migrate_database: no
        mastodon_precompile_assets: no
    
      roles:
    
        - bellackn.mastodon

Known Limitations
-----------------

I have just started using Mastodon, so probably this role is missing some parts that may be crucial for your use case.
PRs welcome!

Things that are missing which I'm aware of:
* Elasticsearch, so no advanced search functionalities
* CI pipeline (Molecule!)

License
-------

MIT

Author Information
------------------

[Nico Bellack](mailto:bellack.n@gmail.com)

[1]:https://blog.joinmastodon.org/2019/10/mastodon-3.0-in-depth/#Whitelist%20mode
