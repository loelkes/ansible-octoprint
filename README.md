Role Name
=========

semuadmin.octoprint

[Ansible role](https://galaxy.ansible.com/semuadmin/octoprint) to deploy OctoPrint and/or mjpg_streamer as systemd services on Raspberry Pi
running stock Raspberry Pi OS 32-bit Lite or Full (Lite is recommended). Should also work
on other Debian distributions though webcam support may depend on the specific hardware.

By default:

- OctoPrint service will be available on: http://host_ip:5000.
- OctoPrint will be installed in the latest stable version. You can select/pin different version
  by setting the `octoprint_version`.
- mjpg_streamer service will be available on: http://host_ip:8080/?action=stream.

(mjpg_streamer can be installed independently of OctoPrint if required)

The user will be prompted to go through the Setup Wizard on accessing the service for the
first time, but a pre-configured config.yaml template is included with standard configuration
items already set up. These can be amended via the OctoPrint admin console.

Based on instructions here:
https://community.octoprint.org/t/setting-up-octoprint-on-a-raspberry-pi-running-raspbian/2337

Contributions welcome - please refer to the [Contributing Guidelines](https://github.com/semuconsulting/ansible_octoprint/blob/master/CONTRIBUTING.md).

Current Status
--------------

![Release](https://img.shields.io/github/v/release/semuconsulting/ansible_octoprint)
![Release Date](https://img.shields.io/github/release-date/semuconsulting/ansible_octoprint)
![Last Commit](https://img.shields.io/github/last-commit/semuconsulting/ansible_octoprint)
![Contributors](https://img.shields.io/github/contributors/semuconsulting/ansible_octoprint.svg)
![Open Issues](https://img.shields.io/github/issues-raw/semuconsulting/ansible_octoprint)
![Downloads](https://img.shields.io/ansible/role/d/42560)

Requirements
------------

Raspberry Pi model 3 or 4 with SSH enabled. If installing on a fresh 'headless' Raspberry
Pi server (e.g. Raspberry Pi OS Lite), add an empty file named 'ssh' to the boot directory
of the SD card to enable remote SSH access. You may also want to set up [SSH key-based
authentication](https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md).

Role Variables
--------------

- `install_octoprint`: true
- `install_mjpg_streamer`: true
- `uninstall_services` : false
- `uninstall_dependencies` : false
- `octoprint_user`: pi (this is the linux user under which the service runs)
- `octoprint_version`: latest
- `install_dir`: "/home/{{ octoprint_user }}"
- `reset_config`: true (set to false to retain existing config.yaml)
- `octoprint_port`: 5000

- `webcam_user`: mjpg_streamer
- `webcam_dir`: "/home/{{ webcam_user }}/mjpg-streamer/mjpg-streamer-experimental"
- `webcam_port`: 8080
- `webcam_type` : "usb" (options are 'usb', 'raspi' or 'custom')
- `webcam_width`: 640
- `webcam_height` : 480
- `webcam_fps`: 10 (frames per second)
- `custom_input` : "input_uvc.so" (input parameters to be used with 'custom' webcam type)
- `webcam_device`: (Optional, not defined by default) Used to specify a device in usb mode, for buggy webcams that present multiple video devices

See https://community.octoprint.org/t/available-mjpg-streamer-configuration-options/1106
for available custom options.

Dependencies
------------

- Python >=3.7

Example Playbook
----------------

```
[your_octoprint_hostname:vars]
ansible_python_interpreter=/usr/bin/python3
```

To install OctoPrint in the latest version and mjpg_streamer with Raspberry Pi camera:

```yaml

    - name: Provision OctoPrint and mjpg_streamer on Raspberry Pi OS
      hosts: your_octoprint_hostname
      remote_user: pi
      become: true

      vars:
        webcam_type: raspi

      roles:
      - semuadmin.octoprint
```

To install OctoPrint with pinned version:

```yaml

    - name: Provision OctoPrint
      hosts: your_octoprint_hostname
      remote_user: pi
      become: true

      vars:
        octoprint_version: "1.8.7"

      roles:
      - semuadmin.octoprint
```

To update OctoPrint, keeping existing configuration and access credentials:

```yaml

    - name: Update OctoPrint with existing configuration
      hosts: your_octoprint_hostname
      remote_user: pi
      become: true

      vars:
        install_octoprint: true
        install_mjpg_streamer: false
        reset_config: false

      roles:
      - semuadmin.octoprint
```

To install just mjpg_streamer with a custom uvc camera configuration:

```yaml

    - name: Provision mjpg_streamer on Raspberry Pi OS
      hosts: your_octoprint_hostname
      remote_user: pi
      become: true

      vars:
        install_octoprint: false
        install_mjpg_streamer: true
        webcam_type: custom
        custom_input: "input_uvc.so -d /dev/video12 -r 1920x1080 -f 15 -q 50"

      roles:
      - semuadmin.octoprint
```

To uninstall OctoPrint, mjpg_streamer and all package dependencies:

```yaml

    - name: Uninstall Octoprint on Raspberry Pi OS
      hosts: your_octoprint_hostname
      remote_user: pi
      become: true

      vars:
        uninstall_services: true
        uninstall_dependencies: true

      roles:
      - semuadmin.octoprint
```

Troubleshooting
---------------

If you get an `[SSL: CERTIFICATE_VERIFY_FAILED]` error when attempting to install this
role on MacOS, this is probably due to changes in the way SSL certificates are packaged
with Python version >=3.6. Try the following:

1. Ensure that the certifi package is at the latest version: `python3 -m pip install --upgrade certifi`.
2. Update the installed certificates using the following command 
(where * is the minor version of Python installed e.g. 3.9):
`/Applications/Python\ 3.*/Install\ Certificates.command`.
3. (*last resort*) Use the -c flag to override certificate validation: `ansible-galaxy install semuadmin.octoprint -c`.

See https://www.python.org/downloads/release/python-360/ for further details (particularly
bullet point 6 under 'Notes on this release').

License
-------

BSD 2-Clause

![License](https://img.shields.io/github/license/semuconsulting/ansible_octoprint)

Author Information
------------------

semuadmin@semuconsulting.com
