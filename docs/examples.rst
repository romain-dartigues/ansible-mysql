########
Examples
########

Basic master-slave setup
########################

.. code-block:: bash

   export ANSIBLE_INVENTORY=inventory.ini
   ssh-add -l >&- || ssh-add
   ansible-playbook site.yml young --diff --check
   ansible-playbook site.yml --limit young --diff --tags mysql_backup --check

Basic master-slave setup tree
=============================

::

   .
   ├── credentials                    # will be created with defaults if unset
   │   └── mysql
   │       ├── betty
   │       │   └── replicator
   │       └── locco
   │           └── root
   ├── group_vars
   │   └── sql.yml
   ├── host_vars
   │   ├── betty.yml
   │   └── young.yml
   ├── roles
   │   ├── ...                        # your other roles
   │   └── mysql                      # this role
   │       └── ...
   ├── ansible.cfg
   ├── inventory.ini
   └── site.yml

group_vars/sql.yml:

.. code-block:: yml

   ---
   mysql_options:
     mysqld:
       bind-address: '::'

host_vars/betty.yml:

.. code-block:: yml

   ---
   mysql_replication_role: 'master'

host_vars/betty.yml:

.. code-block:: yml

   ---
   mysql_replication_role: 'slave'
   mysql_xtrabackup: True

ansible.cfg:

.. code-block:: ini

   [defaults]
   hash_behaviour=merge

inventory.ini:

.. code-block:: ini

   betty ansible_host=betty.example.net
   young ansible_host=young.example.net
   locco ansible_host=localhost

   [sql]
   betty
   young

   [local]
   locco

site.yml:

.. code-block:: yml

   ---
   - hosts: sql
     roles:
       - mysql
     become: yes
