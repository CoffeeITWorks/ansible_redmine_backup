ansible_redmine_backup
=========

setup basic backup on remote host


Role Variables
--------------

    redmine_backup_user: "redmine_backup"
    redmine_backup_password: "backup!password"
    redmine_backup_server: "{{ ansible_hostname }}"

There are more optional vars at `defaults/main.yml` file.

License
-------

MIT

Author Information
------------------
Pablo Estigarribia
