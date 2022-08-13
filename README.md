archlinux-setup
=========

This role aims to perform some basic setups on a fresh install of Arch Linux.  

Requirements
------------

On a minimal install of Arch Linux not even **python** is installed. Make sure to install python as it is needed by Ansible.

Needed:

- ssh connection (because of Ansible obviously)
- python (`sudo pacman -S python`)
- internet access from the Arch Linux system
- community modules:
  - `community.general.pacman`

Role Variables
--------------

You might want to change some variables in order to perform certain actions. A list of common variables to change and an explanation about what they do can be found beneath:

- `flatpak`: If set to `true`, flatpak will be installed and the official repository will be set.
  - default: `false`
- `ssh_agent`: Allows for adding of ssh keys to ssh-agent.
  - default: `true`
  - **Requires** variable `username` to be manually set (e.g. in playbook)
  - Creates a service to be able to add ssh keys to agent
  - Creates bash export (`SSH_AUTH_SOCK`)
  - Creates "~/.ssh/" directory
  - Creates "~/.ssh/config" entry to always add keys to agent
- `desktop`: The desktop environment (**DE**) you want to install and provide basic configuration for.
  - default: `""`
  - Installs DE
  - Installs typical display manager for that DE
  - Supported desktops:
    - `cinnamon`
    - `gnome`
    - `kde` (not yet implemented)
    - `xfce` (not yet implemented)
- `install.cli_useful`: Installs some useful cli tools.
  - default: `false`
  - Installs for example `bind`, `git`, `vim` and `bash-completion`
- `install.desktop_useful`: If a desktop is chosen, also installs some useful graphical applications / useful applications for handling graphical environments.
  - default: `false`
  - Installs for example `gnome-disk-utility`, `gnome-screenshot` and `xorg-xkill`

Dependencies
------------

...

Example Playbook
----------------

Here is an example playbook that install the cinnamon desktop + all optional packages.  
It also provides the user "donien" with the necessary configuration to use add ssh keys to the ssh-agent.  

```yml
---

- name: Use role "archlinux-setup" on machine "ansible-vm-archlinux"
  become: yes
  hosts:
    - ansible-vm-archlinux

  vars:
    username: "donien"
    desktop: "cinnamon"
    install:
      cli_essential: true
      cli_useful: true
      desktop_useful: true

  roles:
    - archlinux-setup

```
