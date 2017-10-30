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

Manually restoring
------------------

Use:

    sudo su redmine
    redmine_back --restore --dropdb

To copy the contents from other server, on backup server:

    rsync /home/redminebackup/backups user@redmineserver:

Then move the files, on redmine server:

    mv /home/redminebackup/backups/ /home/redminebackup/oldbackups/
    mv /home/user/backups/ /home/redminebackup/backups/

Then move the files from the other server and put them as yours

    cd /home/redminebackup/backups
    mv remoteserver myserver

License
-------

MIT

Author Information
------------------
Pablo Estigarribia
