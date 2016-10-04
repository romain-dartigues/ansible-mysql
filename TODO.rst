####
TODO
####

TODO
####

Ansible
=======

Documentation
-------------

YAML documentation, ie: https://github.com/debops/docs/blob/master/docs/conf.py

Passwords generation and Vault
------------------------------

* https://github.com/ansible/ansible/pull/14079
* https://github.com/ansible/ansible/pull/8110

Configure users
---------------

Find a workaround: ansible 2 deprecated using dictionary variables to set all
task parameters, since then the following is not possible:

group_vars/sql.yml::

  mysql_users:
  - {name: reader, password: "pwd123!", priv: '*.*:USAGE'}

tasks/configure.yml::

  - name: configure users
    mysql_user: '{{ item }}'
    with_items: '{{ mysql_users }}'
    when: mysql_users

MySQL
=====

Replication
-----------

* http://www.lexiconn.com/blog/2014/04/how-to-set-up-selective-master-slave-replication-in-mysql/

  * https://support.rackspace.com/how-to/mysql-replication-masterslave/

Auto MySQL Backup
-----------------

* http://askubuntu.com/questions/134670/how-do-i-stop-automysqlbackup-throwing-lock-tables-error
* http://garthwaite.org/automysqlbackup.html


General recommendations to follow
#################################

An Unix user/group for MySQL (ie.: ``useradd -u 27 -g 27 -G 27 -d /home/mysql 
-m -s /bin/bash mysql``).

Filesystem hierarchy (writable by MySQL)::

   /var/run/mysql/data
   /var/run/mysql/backup
   /var/run/mysql/binlog

Admin (root) account must be secured.

Log rotation
============

* ``expire_log_day`` in configuration
* logrotate configuration (for ``slow_queries`` and other logs)

Configuration
=============

.. code-block:: ini

   [mysqld]
   datadir=/lun/mysql1/data
   tmpdir=/lun/mysql1/tmp
   socket=/var/lib/mysql/mysql.sock

   [mysqld_safe]
   log-error=/lun/mysql1/logs/mysqld.log
   slow_query_log_file = /lun/mysql1/logs/mysql-slow.log
   long_query_time=2
   slow-query-log=1

   [mysqld]
   old_passwords=0

   [mysqld]
   # Force use of innodb table partition
   innodb_file_per_table=1

Replication
-----------

The suggested setup is a master-slave configuration.
Both files must be on both server.

master.cnf:

.. code-block:: ini

   [mysqld]
   ; unique per server
   server-id=1
   expire_logs_days=3
   max_binlog_size=20M
   innodb_flush_log_at_trx_commit=1
   sync_binlog=1
   log-bin=/lun/mysql1/binlog/mysql_log-bin_file

slave.cnf:

.. code-block:: ini

   [mysqld]
   ; unique per server
   server-id=2
   skip-slave-start
   read_only=1

Sane defaults (for our setup)
-----------------------------

innodb_buffer_pool_size:
   between 1GB and ⅔ of available memory

innodb_logfile_size:
   25% of innodb_buffer_pool_size

innodb_log_buffer_size:
   25% of innodb_logfile_size

query_cache_size:
   64M to 128M

query_cache_limit:
   1MB to 4MB

table_open_cache:
   64 to 164

table_definition_cache:
   256 to 356

thread_cache_size:
   4
