SickRage
===========
This role deploys [SickRage](http://sickrage.github.io), an automatic Video Library Manager for TV Shows.

Requirements
------------
This role requires Ansible 2.0

Supported Platforms
-------------------
- Ubuntu: 15.04
- Debian: 8
- RHEL/CentOS: 7

Role Variables
--------------
All variables have sensible defaults, which can be found in `defaults/main.yml`.
The current version includes the following variables:
### Defaults

| Name               | Default Value | Description                  |
|--------------------|---------------|------------------------------|
| `sickrage_user_name`  | sickrage | The user to run the SickRage service |
| `sickrage_group_name` | sickrage | The primary group for `sickrage_user_name` to run the SickRage service |
| `sickrage_user_uid` | 1005 | UID of the SickRage service user |
| `sickrage_group_gid` | 1005 | GID of the SickRage service group |
| `sickrage_user_home` | /var/lib/{{ sickrage_user_name }} | home directory for the SickRage service user |
| `sickrage_conf_path` | {{ sickrage_user_home }}/.sickrage | Configuration directory for the SickRage service |
| `sickrage_library_path` | {{ sickrage_user_home }}/data | Root library path, to be used for download directories, tv library etc. |
| `sickrage_port` | 4040 | The TCP port that the SickRage web interface will bind to |
| `sickrage_clone_uri` | 'git://github.com/SickRage/SickRage' | The remote Git repo to clone SickRage from |
| `sickrage_service_file` | | |
| `    src`                  | sickrage.service.j2 | The source template for the SickRage service manifest |
| `    dest`                 | /etc/systemd/system/sickrage.service | The destination to deploy the SickRage service manifest to |
| `sickrage_service_reload_command` | `systemctl daemon-reload` | The command to use when reloading the SickRage service configuration |

### RHEL/CentOS variables
Set in [`vars/RedHat.yml`](vars/RedHat.yml)

|     Name     |     Default Value    |    Description     |
|---------------------------|-----------------------|------------------------------------|
| `sickrage_dependenceis` | - gcc-c++            | A list of dependency packages for SickRage |
|                         | - git                |                                            |
|                         | - make               |                                            |
|                         | - python-cheetah     |                                            |
|                         | - pyOpenSSL          |                                            |

### Debian/Ubuntu variables
Set in [`vars/Debian.yml`](vars/Debian.yml)  

|     Name     |     Default Value    |    Description     |
|---------------------------|-----------------------|------------------------------------|
| `sickrage_dependenceis` | - g++            | A list of dependency packages for SickRage |
|                         | - git-core       |                                            |
|                         | - make           |                                            |
|                         | - python-cheetah |                                            |
|                         | - python-openssl |                                            |

Example Playbook
----------------

    - hosts: sickrage_servers
      roles:
        - role: cmacrae.sickrage

Or, passing parameter values:

	- hosts: sickrage_servers
	  roles:
	    - { role: cmacrae.sickrage, sickrage_user_name: downld, sickrage_group_name: downld }
License
-------
MIT

Author Information
------------------
Created by [Calum MacRae](http://cmacr.ae)

Feel free to:  
Contact me - [@calumacrae](https://twitter.com/calumacrae), [mailto:calum0macrae@gmail.com](calum0macrae@gmail.com)  
[Raise an issue](https://github.com/cmacrae/ansible-sickrage/issues)  
[Contribute](https://github.com/cmacrae/ansible-sickrage/pulls)  
