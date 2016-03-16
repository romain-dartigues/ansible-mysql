######
README
######

.. Important::
   Do not use! In development.

Requirements
############

In your :file:`ansible.cfg`:

.. code-block:: ini

   [defaults]
   hash_behaviour=merge

Conventions
###########

* everything is prefixed with ``mysql_``
* every registerd variable is prefixed by ``mysql_register_``

Credits
#######

Inspiration from:

* https://github.com/akagisho/mysql-replication-ansible
* https://github.com/geerlingguy/ansible-role-mysql

* https://github.com/debops/ansible-mysql
* https://github.com/debops/ansible-mariadb_server
