ansible_redmine_backup
=========

setup basic backup on remote host


Role Variables
--------------

    redmine_backup_user: "redminebackup"
    redmine_backup_password: "$6$jm1S8uJ1VuB$4i9DYTWepvayTwwuO/JNFBhg2dJ0LP0gRyFXelGaLdmU9JRGSLi1EZB/Zncjnz8m0fzt1PPOXoFBwdxVnja3W/"
    redmine_backup_mysqlpass: backup$password
    redmine_backup_server: "{{ ansible_hostname }}"

generate the password with 
 
    mkpasswd -s -m sha-512

default: `backup$password`

There are more optional vars at `defaults/main.yml` file.

License
-------

MIT

Author Information
------------------
Pablo Estigarribia
