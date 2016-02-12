######
README
######

.. Important::
   Do not use! In development.

Credits
#######

Inspiration from:

* https://github.com/akagisho/mysql-replication-ansible
* https://github.com/geerlingguy/ansible-role-mysql

* https://github.com/debops/ansible-mysql
* https://github.com/debops/ansible-mariadb_server

Conventions
###########

* everything is prefixed with ``mysql_``
* every registerd variable is prefixed by ``mysql_register_``
* every tag is prefixed with ``mysql/``

TODO
####

Ansible
=======

Passwords generation and Vault
------------------------------

* https://github.com/ansible/ansible/pull/14079
* https://github.com/ansible/ansible/pull/8110

MySQL
=====

Replication
-----------

* http://www.lexiconn.com/blog/2014/04/how-to-set-up-selective-master-slave-replication-in-mysql/

  * https://support.rackspace.com/how-to/mysql-replication-masterslave/

