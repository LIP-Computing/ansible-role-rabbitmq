# Ansible Role: RabbitMQ

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-rabbitmq.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-rabbitmq)

Installs RabbitMQ on Linux.

## Requirements

(Red Hat / CentOS only) Requires the EPEL repository, which can be installed
with the `geerlingguy.repo-epel` role. 

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

Controls the RabbitMQ daemon's state and whether it starts at boot.

    rabbitmq_daemon: rabbitmq-server
    rabbitmq_state: started
    rabbitmq_enabled: true

The RabbitMQ version install is the one in already provided repositories.

(Debian/Ubuntu only) Controls the .deb to install.

    rabbitmq_deb: "rabbitmq-server_{{ rabbitmq_version }}-1_all.deb"
    rabbitmq_deb_url: "https://packagecloud.io/rabbitmq/rabbitmq-server/packages/{{ ansible_distribution | lower }}/{{ ansible_distribution_release }}/{{ rabbitmq_deb }}/download"

You can enable clustering (*work in progress*), setting this variable to true.

    rabbitmq_cluster: false

If you set `rabbitmq_cluster: true`, set the erlang cookie so it's the sam over all
member of the cluster.

    rabbitmq_erlang_cookie: "set_your_cockie_here"

This is the full path name to the erlang cookie file.

    rabbitmq_erlang_cookie_file: /var/lib/rabbitmq/.erlang.cookie 

List of users to create, and set password.

    rabbitmq_users:
      - user: admin
        password: set_admin_password
        tags: administrator

List of user to remove

    rabbitmq_users_absent:
      - guest

List of `vhosts` to create

    rabbitmq_vhosts: []

List of `vhosts` to remove

    rabbitmq_vhosts_absent: []


## Dependencies

None.

## Example Playbook

    - hosts: rabbitmq
      roles:
        - name: geerlingguy.repo-epel
          when: ansible_os_family == 'RedHat'
        - geerlingguy.rabbitmq

## License

MIT / BSD

## Author Information

This role was created in 2017 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
