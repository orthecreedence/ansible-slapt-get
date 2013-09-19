slapt-get module for Ansible
============================

What up, Slackers. I made this module for slapt-get package deployments using
Ansible. My usual MO is to set up slapt-get to point at a custom (local) package
repo AND at and official repo. This way I can distribute packages to my servers
that take precedence over official packages, but can use the official packages
if there's no custom one.

Works beautifully.

However, Ansible doesn't ship with a slapt-get module. So here it is! My hope
is to eventually get this included with Ansible so Slack becomes an easy
deployment target.

Usage
-----

You can either put the `slapt-get` file in `/usr/share/ansible/packaging/` or
you can put it in a custom folder and point ansible to it via `-M`:

```bash
ansible www -M ./ansible-slapt-get -m slapt-get -a 'pkg=nginx state=present'
```

This module supports ansible's `-C` option (check only, don't make changes).

### Arguments

##### pkg (optional)
Name of the package(s) to operate on. Can be comma-separated.

##### state (optional, default="present")
The state of the package. Possible values: `absent` `present` `latest`

##### update (optional)
Whether or not to update the package sources (`slapt-get --update`) before
running the operation. Can be used standalone:

```bash
ansible www -m slapt-get -a 'update=yes'
```

License
-------

GPL v3
