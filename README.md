## Plone Ansible playbook

## Description

An Ansible project that allows you to provision a full-stack Plone server

### Introduction

Plone's Ansible Playbook can completely provision a remote server to run the full stack of Plone, including:

- Plone in a cluster configuration;
- Automatic starting and process control of the Plone cluster with [supervisor](http://supervisord.org);
- Load balancing of the cluster with [HAProxy](http://www.haproxy.org/);
- Caching with [Varnish](https://www.varnish-cache.org/);
- [Nginx](http://wiki.nginx.org/Main) as a world-facing remote proxy and URL rewrite engine;
- An outgoing-mail-only mail server using [Postfix](http://www.postfix.org/);
- Monitoring and log analysis with [munin-node](http://munin-monitoring.org/) and [logwatch](http://linuxcommand.org/man_pages/logwatch8.html) and [fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page).
- Use of a local [VirtualBox](https://www.virtualbox.org/) provisioned via [vagrant](https://www.vagrantup.com/) to test and model your remote server.

An ansible playbook and roles describe the desired condition of the server. The playbook is used both for initial provisioning and for updating.

We generally support relatively current CentOS and Debian/Ubuntu environments. Versions currently supported are Ubuntu 16.0.4 (Xenial) LTS, Ubuntu 15, Ubuntu 14, Debian wheezy, Debian jessy, and CentOS 7.

See the `docs` subdirectory or [readthedocs](http://plone-ansible-playbook.readthedocs.org/en/latest/) for complete documentation.

Detailed, tutorial-style documentation with lots of real-life examples is available at the [Plone Training](https://training.plone.org/5/deployment/index.html) site.

1. Install a *current* version of Ansible using one or more of the following options:

   ```shell
   pip install ansible
   pip update ansible
   ```

2. If you wish to test locally, install Vagrant and VirtualBox.

3. Run `ansible-galaxy -p roles -r requirements.yml install` to install required roles from scratch.

4. The default `local-configure.yml` includes options for small, medium and multiserver installs. Alternatively you can one of the `sample*.yml` files to `local-configure.yml` and edit as needed.

5. At a minimum you will wnat to change the admin email address and password in  `local-configure.yml` 

6. To test in a local virtual machine, run `vagrant up centos7` or `vagrant provision centos7` to kickoff the configuration of a VM running centos7. Running `vagrant up xenial`will kick off a xenial vm configuration. See the Vagrantfile other options.

7. To deploy, create an Ansible inventory file for the remote host and run `ansible-playbook --ask-sudo-pass -i myhost.cfg playbook.yml`.

8. Configure an appropriate firewall. See included examples for **firewalld** and **ufw**.

Important Note:

If you get connection errors using Ansible, ensure that the remote machine (or VM) has Python 2.7 installed.

### Testing

Once the project has succesfully run you can access the VM's Plone Site using the following URL:

- [http://localhost:7081/Plone/](http://localhost:7081/Plone/)

If https has been properly configured:

- [https://localhost:7081/Plone/](https://localhost:7081/Plone/)



### License

BSD-3-Clause