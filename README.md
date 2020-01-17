# M7011E deployment

This is a fork of [`nodejs-server-ansible-playbook`](https://github.com/JamesTheHacker/nodejs-server-ansible-playbook).

## Prerequisities
* One Ubuntu 18.04 server for the NodeJS application.
* One Ubuntu 18.04 server for the PostgreSQL database.
* A domain served from Digital Ocean with domain names pointing to the servers.
* A SMTP account.

## Preparations
Generate a SSH key called `keys/webdyn-deploy`.

    ssh-keygen

Fill in the following settings.

`group_vars/all.yml`:

* `privileged_db_pw`: Any secret password.
* `restricted_db_pw`: Any secret password.
* `key_url`: A URL to your public SSH key.

`group_vars/db_servers.yml`:

* `user_pass`: Any secret password.

`group_vars/node_servers.yml`:

* `domain`: Your domain.
* `www_domain`: www. + your domain.
* `api_token`: An API token for changing the Digital Ocean DNS zone.
* `user_pass`: Any secret password.
* `email`: Your email.
* `country`: Your ISO 3166-1 alpha-2 code.
* `TunnelTarget`: sql@ + your database domain name.
* SMTP settings in `api_settings`.

`hosts`:

* The domain names for your servers.

## Provision

    ansible-playbook -i hosts db-servers.yml
    ansible-playbook -i hosts node-servers.yml