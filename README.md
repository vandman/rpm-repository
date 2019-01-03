Role Name
=========

This role install conf file for centos repo.
It is intended to be used to create a local repository with reposync and craterepo or not.

Requirements
------------
Access to a repository containing packages, likely on the internet.

Role Variables
--------------

# Where to store downloaded files
cachedir: /var/cache/yum

#CentOS repo are sync from http://vault.centos.org/
#I have setup all repo for x86_64 architecture in the defaults variable file. Just comment the repo you do not need.
#Prior to CentOS 3.7, the reposync command does not work.
#CentOS 6.10 and 7.5.1810 has been excluded as there are only sources.
#No contrib between 5.0 and 5.2
vault_repotosync:
 - { releasever: '3.7', basearch: 'x86_64', repo: ['addons', 'centosplus', 'contrib', 'extras', 'updates'], key: 'RPM-GPG-KEY-CentOS-3'}
 - { releasever: '3.8', basearch: 'x86_64', repo: ['addons', 'centosplus', 'contrib', 'extras', 'updates'], key: 'RPM-GPG-KEY-CentOS-3'}

releasever => CentOS version
basearch => needed architecture (only one per line)
repo => all default repo that follow this link http://vault.centos.org/{{ releasever }}/{{ repo }}/{{ basearch }}
key => this is needed because sometimes it like RPM-GPG-KEY-CentOS-3 ans sometimes like RPM-GPG-KEY-centos3, need te be specified


vault_repotosync_extra:
- releasever: '6.7'
  basearch: 'x86_64'
  repo:
    - name: 'cloud'
      sub: 'openstack-juno'
    - name: 'sclo'
      sub: 'rh'
    - name: 'sclo'
      sub: 'sclo'

releasever => CentOS version
basearch => needed architecture (only one per line)
repo => all default repo that follow this link http://vault.centos.org/{{ releasever }}/{{ repo.name }}/{{ basearch }}/{{ repo.sub }}

epel_repotosync:
 - { releasever: '6', basearch: 'x86_64'}
 - { releasever: '7', basearch: 'x86_64'}

releasever => CentOS version
basearch => needed architecture (only one per line)

pgdp_repotosync:
 - { pgdg: '9.4', pgdgsh: '94', releasever: '5Client', basearch: 'x86_64'}
 - { pgdg: '9.4', pgdgsh: '94', releasever: '5Server', basearch: 'x86_64'}

pgdg => postgresql version
pgdgsh => postgresql short version (without the dot)
releasever => CentOS version
basearch => needed architecture (only one per line)

remi_repotosync:
 - { releasever: '4', repo: '', basearch: 'x86_64'}
 - { releasever: '5', repo: '', basearch: 'x86_64'}

releasever => CentOS version
basearch => needed architecture (only one per line)

ius_repotosync:
 - { releasever: '6', repo: '', basearch: 'x86_64'}
 - { releasever: '6', repo: 'archive', basearch: 'x86_64'}
 - { releasever: '6', repo: 'dev', basearch: 'x86_64'}
 - { releasever: '6', repo: 'testing', basearch: 'x86_64'}

releasever => CentOS version
basearch => needed architecture (only one per line)
repo => link to template file repository

lemonldap_repotosync:
 - { releasever: '7', repo: 'oldstable', extra: 'OK'}
 - { releasever: '7', repo: 'stable', extra: 'OK'}

releasever => CentOS version
repo => version needed
extra => if OK, activate the extra package of lemonldap

Dependencies
------------
None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - role: rpm-repo

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
