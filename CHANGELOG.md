# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2024-01-11

### Added

* Verify that the port is open and the service is running after installation.
* Verify that `octoprint.user` and `octoprint.group` exist on the target.
* Check that ansible has root privileges on the target.
* Check that systemd is available.

### Removed
* Support for mjpeg-streamer.
* Configure OctoPrint with a `config.yml` template with the `reset_config` variable. This may be added back in a different form in a future release.

### Changed
* Structure and naming of variables.
* Role structure.
* `install_dir`, now `octoprint.dir` has a default value of `/srv/octoprint`.
* The functionality of `install_octoprint`, `uninstall_services` and `uninstall_dependencies` are combined in the logic of `octoprint.state`.

## [1.x.x]

No changelog provided.