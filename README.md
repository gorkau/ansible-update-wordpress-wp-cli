# ansible-update-wordpress-wp-cli

Automates the process of updating WordPress blogs in several domains/servers by using Ansible (https://docs.ansible.com/) and WP-Cli (https://wp-cli.org/).

I have only tried in Ubuntu. Not sure if Ansible works in Windows.

Disclaimer: You should be careful with any script you use. It is always unsafe to installa anything you have not properly reviewed.

## Installation

### Prerequisites

You must have ansible installed in your system. See: https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

### Download or clone this project

You may download it to any folder in your computer.

### Create your roles/update-blogs/vars/main.yml file

```
wpcliuser: valid_username_in_the_server
wpcligroup: valid_group_in_the_server
wpclipath: /usr/local/bin/wp
projects:
    mydomain.com:
        blog_folder: /var/www/mydomain.com/
```     
### Modify /etc/ansible/hosts

Add a section called [blogs]:

```
[blogs]

mydomain.com
```

NOTE: Only the domains in this folder will be updated.

## Usage

Run it from the folder where you have your wp.yml file.

### Normal usage

$ ansible-playbook wp.yml

### If you want to install WP-Cli

$ ansible-playbook wp.yml --extra-vars "installcli=true" -K

NOTE: If I were you I would install this manually in your server. Just added it for very lazy people.

### If you want mayor WordPress version updates

$ ansible-playbook wp.yml --extra-vars "major=true"

## TODO

* Backup all the files before updating.
* The database backup is always using the same file. I would like to use a different file every time. And maybe download them compressed and delete the old ones.

## If you do not like WP-Cli

Peter (??) created this script that does not use WP-Cli, just plain Ansible:

https://www.petersplanet.nl/index.php/2017/12/10/automate-wordpress-updates-with-ansible/
