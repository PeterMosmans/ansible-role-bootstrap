Ansible Role: Bootstrap
=======================

Build status for this role: [![Build Status](https://travis-ci.org/PeterMosmans/ansible-role-bootstrap.svg)](https://travis-ci.org/PeterMosmans/ansible-role-bootstrap)


This role bootstraps a (new) server into existence. It installs and tightens a firewall, hardens SSH and modifies GRUB. The main focus is on **hardening a fresh server installation**.


Requirements
------------

None.

Role Variables
--------------

Available variables are listed below, along with default values



**bootstrap_commands**: A list with commands that will be executed on the host as last step of the bootstrap role. Example:
``` 
bootstrap_commands:
- "sudo /usr/bin/compact_box.sh"
```


**bootstrap_directories**: A list with directories and files that will be created along with permissions, owner and groups. Example:
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


**bootstrap_files**: A list with files that will be copied to the target machine. Example:
```
bootstrap_files:
- src: my-file.py
  dest: /tmp/my-file.py
   mode: "0755"
```


**bootstrap_git_repositories**: A list with common git repositories that will be cloned. Example:
```
bootstrap_git_repositories:
 - repo: https://github.com/PeterMosmans/security-scripts
   dest: /var/git/security-scripts
   version: master
```


**bootstrap_groups**: A list with usergroups that will be added by default. The defaults can be found in `defaults/main.yml`:
```
bootstrap_groups:
  - git
  - sudo
```


**bootstrap_users**: A nested lists with users to add, with their SSH key, and optional git repos to install (for e.g. dotfiles), and installers to run (for e.g. setting up symlinks).
Example:
```
bootstrap_users:
 - name: apenut
   comment: "Ape Nut"
   groups:
     - git
     - sudo
   shell: "/bin/bash"
   ssh_key: https://github.com/your-github-username.keys
   repos:
     - src: https://github.com/your-github-username/dotfiles
       dest: /home/apenut/.dotfiles
       version: master
   installers:
     - command: /home/apenut/.dotfiles/installer.sh
```
If you don't want to add any repositories or installer scripts, You can also leave the `repos` and `installers` variables empty:
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


**bootstrap_packages**: A list with packages that will be installed by default. The defaults can be found in `defaults/main.yml`:
```
bootstrap_packages:
  - aptitude
  - ca-certificates
  - curl
  - git
  - locate
  - lsof
  - ntp
  - openssl
  - sudo
  - tmux
  - ufw
  - unzip
  - zsh
```


**bootstrap_packages_remove**: A list with packages that will be removed by default. The defaults can be found in `defaults/main.yml`:
```
bootstrap_packages_remove:
  - bluez
  - crda
  - cups
  - iso-codes
  - iw
  - libiw30
  - task-laptop
  - wireless-regdb
  - wireless-tools
  - wpasupplicant
```


**bootstrap_pip_packages**: A list with pip packages that will be installed globally by default. Example:
```
bootstrap_pip_packages:
  - ansible
```


**bootstrap_sudo_users**: A lists of users to grant passwordless access to sudo using the `/etc/sudoers` file. Example:
```
bootstrap_sudo_users:
  - vagrant
```


**bootstrap_ufw_tcp_allow**: A list of TCP ports that will be opened up in the firewall. It defaults to port 22 only. Example:
```
bootstrap_ufw_tcp_allow:
  - 22
  - 80
  - 443
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


#### sshd_config
The following (Jinja) variables will be applied to the SSH daemon template file in `templates/sshd_config.j2`. The defaults can be found in `defaults/main.yml`:
```
sshd_banner: /etc/issue.ssh
sshd_ciphers: "chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr"
sshd_gssapiauthentication: "no"
sshd_hostkeyalgorithms: "ssh-ed25519-cert-v01@openssh.com,ssh-rsa-cert-v01@openssh.com,ssh-ed25519,ssh-rsa"
sshd_kexalgorithms: "curve25519-sha256@libssh.org,diffie-hellman-group-exchange-sha256"
sshd_macs: "hmac-sha2-512-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-ripemd160-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-512,hmac-sha2-256,hmac-ripemd160,umac-128@openssh.com"
sshd_passwordauthentication: "no"
sshd_permitemptypasswords: "no"
sshd_permitrootlogin: "no"
sshd_pubkeyauthentication: "yes"
sshd_rsaauthentication: "yes"
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
