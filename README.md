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

Copying the files from remote server (ex: production to testing)
----------------------------------------------------------------

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


Example restoring from test server to prod server
-------------------------------------------------

**Test server name:** TESTSERVER
**Prod server name:** PRODSERVER
**Backup server name:** BACKUPSERVER

Restore production on test server:

Login to test server TESTSERVER

:$ sudo su redminebackup

:$ cd /home/redminebackup

:$ mv backups oldbackups

# Copy files from prod:
:/home/redminebackup$ rsync -ahlu redminebackup@BACKUPSERVER:/home/redminebackup/backups/ backups/

# We will restore on test server TESTSERVER so, we will rename the backups of prod server PRODSERVER to TESTSERVER to be used during restore.
:/home/redminebackup$ cd backups/
:/home/redminebackup/backups$ rm -rf TESTSERVERold
:/home/redminebackup/backups$ mv TESTSERVER TESTSERVERold
:/home/redminebackup/backups$ mv PRODSERVER TESTSERVER
:$ exit

# Restore:
:$ sudo su redmine
:/home/redminebackup/backups$ redmine_back --restore --dropdb

# Plugins:
$ cd /opt/redmine/current/plugins
:/opt/redmine/current/plugins$ source /usr/local/rvm/scripts/rvm && bundle install
:/opt/redmine/current/plugins$ source /usr/local/rvm/scripts/rvm && rake db:migrate RAILS_ENV=production

:/opt/redmine/current/plugins$ source /usr/local/rvm/scripts/rvm && rake redmine:plugins:migrate RAILS_ENV=production


# Restart apache:

- Login to TESTSERVER
- Disable notifications
	- Change hostname and path   - TESTSERVER.YOURDOMAIN.NET
Change application title
