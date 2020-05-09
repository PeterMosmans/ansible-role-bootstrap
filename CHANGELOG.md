# Changelog

All notable changes to this project will be documented in this file. See [standard-version](https://github.com/conventional-changelog/standard-version) for commit guidelines.

## [1.6.0](https://github.com/PeterMosmans/ansible-role-bootstrap/compare/v1.5.0...v1.6.0) (2020-05-09)


### Features

* allow SSH key configuration using user module ([ba15fa6](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/ba15fa6fbe6cc30c81825badf0695c797b54570e))
* use nicer labels when looping user-related tasks ([5cca6dd](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/5cca6ddeec73eff5ad9a8da784e703dbb528e3bb))


### Bug Fixes

* properly deal with loops and empty sublists ([1e46633](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/1e466333325353b2481b74bde0a464f9fbb14cef))
* revert earlier pipefail ansible-lint fix ([30048a4](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/30048a4abb6c81d543bcb497dce4caac926f7d58))
* set pipefail option for shell command ([d3a2be2](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/d3a2be2006fa34922e5f778d00c34fd2e049a928))
* set timezone using native Ansible module ([a61c767](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/a61c767287cfd330ea055840199f01ba8ac8e045))

## [1.5.0](https://github.com/PeterMosmans/ansible-role-bootstrap/compare/v1.4.1...v1.5.0) (2020-04-30)


### Features

* support mounts and update-alternatives ([9a4d621](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/9a4d6214954c495efa7cc0e409446f29633d1757))

### [1.4.1](https://github.com/PeterMosmans/ansible-role-bootstrap/compare/v1.4.0...v1.4.1) (2020-04-17)

## 1.4.0 (2020-04-17)


### Features

* add autoclean to update step ([f83e27e](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/f83e27e08727fa005dac2fee7160c466e9a63199))
* add installation of third-party packages ([a0db8b6](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/a0db8b6627caa779b477c751b59e13ee1cf665f2))


### Bug Fixes

* ensure strings are properly quoted ([5bf7129](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/5bf7129ff00a796ba9a52e2b62d55fe6cbfd92b7))
* ensure that strings are properly parsed ([0e094a8](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/0e094a881bf71ca16c403a8ba16de5ae2b711895))
