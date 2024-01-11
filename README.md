ansible-octoprint
=================

![Release](https://img.shields.io/github/v/release/loelkes/ansible-octoprint)
![Release Date](https://img.shields.io/github/release-date/loelkes/ansible-octoprint)
![Last Commit](https://img.shields.io/github/last-commit/loelkes/ansible-octoprint)
![Contributors](https://img.shields.io/github/contributors/loelkes/ansible-octoprint.svg)
![Open Issues](https://img.shields.io/github/issues-raw/loelkes/ansible-octoprint)
![License](https://img.shields.io/github/license/loelkes/ansible-octoprint)

[Ansible role](https://galaxy.ansible.com/loelkes/octoprint) to deploy OctoPrint as systemd services on Debian (or similar, like Raspbian, Ubuntu).

The configuration file is not managed by this role as of now . It will be deleted if the state is set to `absent` in the variables. The restart commands are configured through the OctoPrint configuration CLI.

*Note*: This role and repository should not contain any help or advice on octoprint/ansible/linux/raspberrypi configuration. Please see the manuals for the respective projects for help.

Requirements
------------

Debian or similar host with SSH enabled. The user used for ansible must be able to perform sudo commands without password.

Role Variables
--------------

```yaml
octoprint:
  port: 5000 # Port for OctoPrint
  user: pi # System user running OctoPrint. Must already exist, not managed by this role.
  group: pi # System group running OctoPrint. Must already exist, not managed by this role.
  version: latest # OctoPrint Version.
  state: present # Set to absent to remove all files, configurations and services.
  dir: /srv/octoprint # OctoPrint installation directory.
```

Examples
--------

To install OctoPrint in the latest version:

```yaml
    - name: Provision OctoPrint
      hosts: rpi-octoprint
      remote_user: pi
      become: true
      roles:
      - loelkes.octoprint
```

To install OctoPrint with pinned version:

```yaml
    - name: Provision OctoPrint
      hosts: rpi-octoprint
      remote_user: pi
      become: true
      vars:
        octoprint:
          version: "1.8.7"
      roles:
      - loelkes.octoprint
```

To update OctoPrint, keeping existing configuration and access credentials:

```yaml
    - name: Update OctoPrint with existing configuration
      hosts: rpi-octoprint
      remote_user: pi
      become: true
      roles:
      - loelkes.octoprint
```

To uninstall OctoPrint and all package dependencies:

```yaml
    - name: Uninstall OctoPrint on Raspberry Pi OS
      hosts: rpi-octoprint
      remote_user: pi
      become: true
      vars:
        octoprint:
          state: absent
      roles:
      - loelkes.octoprint
```

Contributing
------------

See [Contributing Guidelines](https://github.com/loelkes/ansible-octoprint/blob/master/CONTRIBUTING.md)

License
-------

[BSD 2-Clause](LICENSE)

Changelog
---------

See [CHANGELOG.md](CHANGELOG.md)

Authors
------------------

* [Christian Lölkes](https://github.com/loelkes)
* [semuadmin@semuconsulting.com](mailto:semuadmin@semuconsulting.com)
