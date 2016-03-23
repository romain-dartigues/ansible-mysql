######
README
######

.. Important::
   Still in experimental stages, use at your own risks.

Requirements
############

* ansible
* a GNU userland
* in your :file:`ansible.cfg`:

.. code-block:: ini

   [defaults]
   hash_behaviour=merge

Conventions
###########

* everything is prefixed with ``mysql_``
* every registered variable is prefixed by ``mysql_register_``

Resources
#########

* http://docs.ansible.com/ansible/
* https://sourceforge.net/projects/automysqlbackup/
* https://mariadb.com/kb/en/mariadb/documentation/
* https://dev.mysql.com/doc/
* https://www.percona.com/doc/percona-xtrabackup/

Credits
#######

Inspiration from:

* https://github.com/akagisho/mysql-replication-ansible
* https://github.com/geerlingguy/ansible-role-mysql

* https://github.com/debops/ansible-mysql
* https://github.com/debops/ansible-mariadb_server
