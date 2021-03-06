# Ansible Playbook for deploying WordPress on remote Ubuntu

This deploys a LAMP stack on Ubuntu 14.x (tested, probably works on others too) 
including PHP 5.5, Apache, and MySQL >= 14. It also migrates a wordpress
installation (comprising a mysqldump file and .tar.gz of a wp-content directory)
to the new server. This is only for populating a new server or
completely overwriting an existing WordPress installation. It's useful for
initial deployments and deploying demo versions.

To use, get a mysqldump file of the site to migrate and a .tar.gz of the site's
wp-content directory. Copy each of the files ending in .sample to the same name
without an extension:

    cp ./hosts.sample ./hosts
    cp ./group_vars/dbservers.sample ./group_vars/dbservers
    cp ./group_vars/webservers.sample ./group_vars/webservers
    cp ./group_vars/wordpress.sample ./group_vars/wordpress

and populate the variables described inside each of the renamed files:

    ./hosts
    ./group_vars/dbservers
    ./group_vars/webservers
    ./group_vars/wordpress

The variables include passwords, keys, and other information that should be kept
secret. They have been added to the .gitignore file to prevent accidental
uploads, and you should also consider using [Ansible
Vault](http://docs.ansible.com/playbooks_vault.html) to encrypt their contents.

Based heavily on lamp\_simple from
[ansible-examples](https://github.com/ansible/ansible-examples/)
