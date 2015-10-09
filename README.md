A Simple Ansible Playbook for Django
====================================

This project contains the simplest possible
[ansible](http://docs.ansible.com/ansible) playbook to provision a server for a
django project and deploy new versions of the project.

### Assumptions

This playbook assumes you have created an Ubuntu 14.04 server and have already
set up ssh public key authentication on it. You can easily set up public key
authentication on your server with this command:

`ssh-copy-id root@xxx.xxx.xxx.xxx`

It also assumes you are cool with Postgresql as your database.

### How to use

- Install ansible 1.9.3 or greater on your computer.
- Clone this project.
- Edit the `ansible/hosts` file and enter the IP address of the server you are
	deploying to.
- Edit the `ansible/vars.yml` file and enter values appropriate for your project.
- Run the playbook:

	```
	cd ansible
	ansible-playbook -i hosts provision.yml
	```	

That's it! Your project is now up and running and assuming you've set up a DNS
record for your server, you can now visit your site.

As you make changes and commit to your django project you'll obviously want to
push the new version to production, so to do that without having to run the
full playbook, you can run this command (from the `ansible` directory):
`ansible-playbook -i hosts deploy.yml`

That will check out the latest version of your code, install any new
dependencies via pip if necessary, run the `migrate` and `collectstatic` django
management commands, and restart nginx and gunicorn if necessary.
