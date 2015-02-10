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
    cp ./group\_vars/dbservers.sample ./group\_vars/dbservers
    cp ./group\_vars/webservers.sample ./group\_vars/webservers
    cp ./group\_vars/wordpress.sample ./group\_vars/wordpress

and populate the variables described inside each of the renamed files:

    ./hosts
    ./group\_vars/dbservers
    ./group\_vars/webservers
    ./group\_vars/wordpress

The variables include passwords, keys, and other information that should be kept
secret. They have been added to the .gitignore file to prevent accidental
uploads, and you should also consider using [Ansible
Vault](http://docs.ansible.com/playbooks_vault.html) to encrypt their contents.

Based heavily on lamp\_simple from
[ansible-examples](https://github.com/ansible/ansible-examples/)
