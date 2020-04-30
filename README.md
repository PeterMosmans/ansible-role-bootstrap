Ansible Role: Bootstrap
=======================

Build status for this role: [![Build Status](https://travis-ci.org/PeterMosmans/ansible-role-bootstrap.svg)](https://travis-ci.org/PeterMosmans/ansible-role-bootstrap)


This role bootstraps a (new) server into existence. It installs and tightens a
firewall, hardens SSH and modifies GRUB. The main focus is on **hardening a
fresh server installation**.


Requirements
------------

None.

Role Variables
--------------

Available variables are listed below alphabetically, along with default values.

**bootstrap_alternatives**: A list with alternatives, to manage symbolic links
using the ``update-alternatives`` tool. Example:
```
bootstrap_alternatives:
  - link: /usr/bin/pip
    name: pip
    path: /usr/bin/pip3
```

**bootstrap_commands**: A list with commands that will be executed on the host
as last step of the bootstrap role. Example:
```
bootstrap_commands:
- "sudo /usr/bin/compact_box.sh"
```


**bootstrap_directories**: A list with directories and files that will be
created along with permissions, owner and groups. Example:
```
bootstrap_directories:
 - path: /var/git
   mode: "2660"
   owner: root
   group: git
 - path: /tmp/empty
   mode: "0777"
   owner: root
   group: root
   state: touch
```


**bootstrap_files**: A list with files that will be copied to the target
machine. Example:
```
bootstrap_files:
- src: my-file.py
  dest: /tmp/my-file.py
   mode: "0755"
```
This will be provisioned when the `files` tags is being used.

**bootstrap_git_repositories**: A list with common git repositories that will be
cloned. Example:
```
bootstrap_git_repositories:
 - repo: https://github.com/PeterMosmans/security-scripts
   dest: /var/git/security-scripts
   version: master
```

Note that when this variable is set, the git package needs to be installed, or
part of the **bootstrap_packages** list.

**bootstrap_groups**: A list with user groups that will be added by default. The
defaults can be found in `defaults/main.yml`:
```
bootstrap_groups:
  - sudo
```


**bootstrap_groups_remove**: A list with groups that will be removed by default.
The defaults can be found in `defaults/main.yml`:
```
bootstrap_groups_remove:
  - bluetooth
```


**bootstrap_locale**: The locale to use (e.g. en_US.UTF-8). If not set, it will
default to en_US.UTF-8. Example: ``` bootstrap_locale: "en_US.UTF-8" ``` Note
that this needs the locale package to properly function. If the package isn't
available, the role will still continue.

**bootstrap_mounts**: A list of mounts that will be added to the mount file
(`/etc/fstab`). Example:
```
bootstrap_mounts:
  - path: /home/peter/demos
    src: demos
    fstype: vboxsf
    opts: auto,rw,uid=1000,gid=1000
    state: present
```
This will be provisioned when the `mounts` tags is being used.

**bootstrap_reboot_allowed**: Whether Ansible is allowed to perform a reboot, if
the kernel version has changed, or when the network has become 'unresponsive'
(for instance after a hostname change). The default is false.


**bootstrap_users**: A nested lists with users to add, with their SSH key, and
optional: encrypted password, git repos to install (e.g. dotfiles), and installers to run (e.g.
setting up symlinks). Example:
```
bootstrap_users:
 - name: apenut
   comment: "Ape Nut"
   groups:
     - git
     - sudo
   password: "$6$Qpc015eEs$4Eav1QM.omXm8bD7DFOTNQx6L3SG47vDT8JuMfW15e5gNbgq/C6D/7ZRdH4qoGLi0AW/HBWjJ/pm1thSQPK.e0"
   shell: "/bin/bash"
   ssh_key: https://github.com/your-github-username.keys
   repos:
     - src: https://github.com/your-github-username/dotfiles
       dest: /home/apenut/.dotfiles
       version: master
   installers:
     - command: /home/apenut/.dotfiles/installer.sh
```
If you don't want to add any password, repositories or installer scripts, You can also
refrain from adding the `password` value, and leave the `repos` and `installers`
variables empty. The rest of the variables are required per user though.
```
boostrap_users:
 - name: apenut
   comment: "Ape Nut"
   groups:
     - git
     - sudo
   shell: "/bin/bash"
   ssh_key: https://github.com/your-github-username.keys
   repos: []
   installers: []
```


**bootstrap_packages**: A list with packages that will be installed by default.
The defaults can be found in `defaults/main.yml`:
```
bootstrap_packages:
  - git
  - python3-pip
  - sudo
  - ufw
```

**bootstrap_packages_remove**: A list with packages that will be removed by
default. The defaults can be found in `defaults/main.yml`:
```
bootstrap_packages_remove:
  # packages not needed on bare metal
  - acpid
  - bluez
  - crda
  - discover
  - discover-data
  - eject
  - iw
  - laptop-detect
  - powertop
  - task-laptop
  - wireless-regdb
  - wireless-tools
  - wpasupplicant
  # several superfluous packages
  - console-setup
  - cups
  - dictionaries-common
  - installation-report
  - iso-codes
  - ispell
  - krb5-locales
  - man-db
  - manpages
  - nano
  - shared-mime-info
  - task-english
  - util-linux-locales
  - wamerican
  - xkb-data
  - xz-utils
```


**bootstrap_pip_packages**: A list with pip packages that will be installed globally by default. Example:
```
bootstrap_pip_packages:
  - ansible
```

Note that **pip** (e.g. `python3-pip`) needs to be installed for this, so don't
forget to add that to the **bootstrap_packages** list.

**bootstrap_pip_version**: The version of pip to be used. This defaults to pip3
whennot specified but can be overridden.

**bootstrap_sudo_users**: A lists of users to grant passwordless access to sudo using the `/etc/sudoers` file. Example:
```
bootstrap_sudo_users:
  - vagrant
```


**bootstrap_ufw_tcp_allow**: A list of TCP ports that will be opened up in the firewall. It defaults to port 22 only. Example:
```
bootstrap_ufw_tcp_allow:
  - "22"
  - "80"
  - "443"
```

Note that when this variable is set, the ufw package needs to be installed, or
part of the **bootstrap_packages** list.


**bootstrap_url_packages**: A list of URLs that will be installed as packages.
Example:
```
bootstrap_url_packages:
- https://github.com/sharkdp/bat/releases/download/v0.12.1/bat_0.12.1_amd64.deb
```

**grub_settings**: A list of name / value pairs that will be applied to the GRUB config file. The defaults can be found in `defaults/main.yml`:
```
grub_settings:
  - name: "GRUB_TIMEOUT"
    value: "0"
  - name: "GRUB_RECORDFAIL_TIMEOUT"
  value: "0"
```


**hostname**: The hostname for the machine. If none is given, it will default to "bootstrapped". Example:
```
hostname: bootstrapped
```



**sshd_moduli_remove**: A list of moduli values that will be removed from the /etc/ssh/moduli list. The defaults can be found in `defaults/main.yml`:
```
sshd_moduli_remove:
  - 1023
  - 1535
```


**timezone**: The timezone for the machine. The default can be found in `defaults/main.yml`:
```
timezone: Etc/UTC
```

## Templates

**bootstrap_templates**: A list with templates that will be applied and deployed.  The defaults can be found in `defaults/main.yml`:
```
bootstrap_templates:
  - src: hosts.j2
    dest: /etc/hosts
    mode: "0644"
  - src: issue.ssh.j2
    dest: /etc/issue.ssh
    mode: "0644"
  - src: locale.j2
    dest: /etc/default/locale
    mode: "0644"
  - src: sshd_config.j2
    dest: /etc/ssh/sshd_config
    mode: "0644"
```


The following templates will be applied and deployed by default:

#### hosts
The template `templates/hosts.j2` will be copied to the host. The list of IP - name pairs in the variable `bootstrap_hostsfile` will be deployed. Example:
```
bootstrap_hostsfile:
  - ip: 127.0.0.1
    name: mywebsite
```


#### issue.ssh
The template `templates/issue.ssh.j2` will be copied to the host, and applied as SSH banner using the **company** variable. Change the text to something that applies to you(r company). The default can be found in `defaults/main.yml`:
```
company: "Go Forward"
```


#### locale
The template `templates/locale.j2` will be copied to the host, and contain the correct bootstrap_locale string(s).


#### sshd_config
The following (Jinja) variables will be applied to the SSH daemon template file in `templates/sshd_config.j2`. The defaults can be found in `defaults/main.yml`:
```
sshd_acceptenv: LANG LC_*
sshd_banner: /etc/issue.ssh
sshd_ciphers: "chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr"
sshd_gssapiauthentication: "no"
sshd_hostkeyalgorithms: "ssh-ed25519-cert-v01@openssh.com,ssh-rsa-cert-v01@openssh.com,ssh-ed25519,ssh-rsa"
sshd_kexalgorithms: "curve25519-sha256@libssh.org,diffie-hellman-group-exchange-sha256"
sshd_macs:
"hmac-sha2-512-etm@openssh.com,hmac-sha2-256-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-512,hmac-sha2-256,umac-128@openssh.com"
sshd_maxauthtries: 2
sshd_passwordauthentication: "no"
sshd_permitemptypasswords: "no"
sshd_permitrootlogin: "no"
sshd_pubkeyauthentication: "yes"
sshd_usedns: "no"
sshd_usepam: "yes"
sshd_x11forwarding: "no"
```


Dependencies
------------

None.



Example Playbook
----------------
```
- hosts: all
  become: yes
  become_method: sudo
  roles:
  - role: PeterMosmans.bootstrap
  vars:
  hostname: "myhostname"
```
This example will harden SSH, configure GRUB, and name the host "myhostname"



License
-------

GPLv3


Author Information
------------------

Created by Peter Mosmans.
