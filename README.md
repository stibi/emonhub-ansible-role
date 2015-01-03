# emonhub on RaspberryPi Ansible role

This role install and configures an [emonhub](https://github.com/emonhub/emonhub) node on your RaspberryPi.

## Requirements

This role requires Ansible 1.7 or higher and platform requirements are listed in the metadata file.

## Support

I have tested this role on a RaspberryPi running on Archlinux ARM.
I'd be happy for someone who would run the role also on Raspi with Raspbian. The role is prepared for multi os support, it's just about to adjust the content of variable files for each system. You can see `Archlinux.yml` and `Raspbian.yml` in `vars/`.
You know, pull requests are welcome…

## Role Variables

### Distro specific variables 

Some distro specific variable are imported for a play on runtime.
The property names are quite self describing I think, so for example the `vars/Archlinux.yml`:

```
emonhub_ansible_role_distro_vars:
  emonhub_packages:
    - python2
    - python2-pyserial
    - python2-configobj
  emonhub_user_groups:
    - users
    - uucp
```

`emonhub_packages` : this is a list emonhub dependencies, needed to be installed by package manager on the system
`emonhub_user_groups` : a list of groups, to which a non-priviledged user is assigned, under this user is emonhub running

### Role variables

The you can setup few role variables, see the usage in examples.

`rfm12pi_group` : the network group for RFM12B modules communication 
(if not specified, the default is `210`) 

`rfm12pi_freq` : the frequency on which RFM12B modules communicates 
(if not specified, the default is `868`) 

`fm12pi_baseid` : the base ID of a RFM12Pi module on your raspi
(if not specified, the default is `1`) 

`emonhub_emoncms_apikey` : the apikey for communication with EmonCMS
(no default value, must be specified)

### Other vars

Finally, a handfull of the usual variables in `vars/main.yml`:

`emonhub_user` : name of the non-priviledged user used to run emonhub
`users_group` : name of system group for users
`emonhub_repo_installation_dir` : path to where is the emonhub repository cloned in the system
`emonhub_installation_dir` : path where is the emonhub actually installed
`emonhub_config_path` : path to where is the emonhub config file stored
`emonhub_logfile` : path to emonhub logfile
`python_exec_path` : path yo python2 executable, needed for emonhub systemd server, will be moved to Archlinux specific variable file (TODO)

Dependencies
------------

Nope, nothing.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
- name: Configure my RaspberryPi
  hosts: myraspi
  roles:
    - { role: emonhub-ansible-role, rfm12pi_group: 210, rfm12pi_freq: 868,rfm12pi_baseid: 1, emonhub_emoncms_apikey: "6a345ec65137009a59e4f56bfabb4f3e" }
```

License
-------

BSD

Author Information
------------------

Martin Stiborský (CZ)
Twitter: http://twitter.com/stibi
G+: https://plus.google.com/+MartinStiborsky 
