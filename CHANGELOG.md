# Changelog

## [2.4.0](https://github.com/PeterMosmans/ansible-role-bootstrap/compare/2.3.0...2.4.0) (2022-04-12)

### Features

- add files tags to provision files
  ([3be8151](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/3be815179fe9c54eebc73e79f5d3b77007eec48f))
- ensure proper line endings
  ([93fe434](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/93fe434ecfdcea77daf536c3bda639901bc96ab1))
- rename locale setting
  ([7bbe205](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/7bbe205d410001388e41040add372a673987d7e8))
- support group parameter for files and templates
  ([7f068a9](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/7f068a9897db6a2b30c8b1170848d93cd32996b6))
- update hostsfile with more sane defaults
  ([bdb0de5](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/bdb0de5ca5548966261a2ff79980c6ee5101fa37))

### Bug Fixes

- import tasks to ensure tags can be used
  ([6f3ba5d](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/6f3ba5d064dd52c724551a05dbdf2d4ff999246f))
- use FQDN everywhere, and true / false for truthy values
  ([cfdac61](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/cfdac6108534ccad137445db086b654016f68147))

## [2.3.0](https://github.com/PeterMosmans/ansible-role-bootstrap/compare/v2.2.0...v2.3.0) (2022-01-27)

### Features

- ensure more robust empty var handler
  ([797217f](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/797217fa644249330c9b506c8226058dad75d072))
- ensure more robust error handling
  ([a10aa75](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/a10aa75e98c4fc136df7a426627cda27a75c789c))
- ensure users in sudo group don't need password
  ([ad80c41](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/ad80c413c0c0642df0374996dea0a9fb9831f18a))
- only show changed when non-zero resultcode
  ([4a3586d](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/4a3586db55f159c5f85bfce044f4faa62cac663f))
- remove stale default value
  ([ad9e32c](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/ad9e32cab4b1ffda00f8c480592f772f75d405ec))
- use correct include syntax
  ([d493867](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/d4938677eba995d4a0c449677b3604abc12de753))
- use fully qualified names and defaults
  ([822d462](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/822d462255726ada3be323050d197aac863574ba))
- use inventory_hostname to set hostname
  ([07b6b21](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/07b6b214863cf08c743c1b38e34b85cc414aa495))
- use newer loop syntax
  ([4ba0031](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/4ba00318c04464516822a85662a8d4372ae13a19))

## [2.2.0](https://github.com/PeterMosmans/ansible-role-bootstrap/compare/v2.1.0...v2.2.0) (2021-06-01)

### Features

- allow selective disabling of certificate validation
  ([6b8b0bc](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/6b8b0bca6e8fb704c33aa1ce6c8016cb4e50f8c3))
- move ufw firewall defaults to defaults file
  ([388e400](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/388e40048198f429c31a9334a2429dc5b33cf9a5))
- only set version for git repository when specified
  ([540647c](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/540647ccc29474a0008c264feb0e0881d0b2c9b4))

### Bug Fixes

- only install Python packages when necessary
  ([ee07f9a](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/ee07f9a3e5253a4962ad5d7779307bd09a0b2f63))

## [2.1.0](https://github.com/PeterMosmans/ansible-role-bootstrap/compare/v2.0.0...v2.1.0) (2020-07-16)

### Features

- show nice labels during loops
  ([39feefd](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/39feefd9105ad97baac0071131d286a56e89c683))
- support supplying a gid for new groups
  ([cf2a079](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/cf2a0792568ca4b0f80b3492511f0df01c3c843c))
- support supplying SSH key size for new users
  ([b015cfa](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/b015cfa28505ea33de89b44604a7df531d8f2a29))
- use Ansible defaults instead of hardcoded values
  ([67e0ad5](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/67e0ad5009506da400f5c717bf72e06e466f136f))

## [2.0.0](https://github.com/PeterMosmans/ansible-role-bootstrap/compare/v1.6.0...v2.0.0) (2020-05-09)

### ⚠ BREAKING CHANGES

- This is incompatible with the previous bootstrap_groups list, as this now
  expects a name key, and an optional system key.

Previous situation:

bootstrap_groups:

- docker
- mygroup

New situation:

bootstrap_groups:

- name: docker system: yes
- name: mygroup

### Features

- add ability to create system accounts
  ([19b90b6](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/19b90b64b00e229e7695b4a13ac1ebff633be227))
- enable groups to be system groups
  ([5861c2a](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/5861c2a2d04552f69a1b610b10699528754a119a))
- use Ansible defaults when certain parameters aren't set
  ([fec6328](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/fec632875a6eb8caf6c0a99103b7711c678a076b))

## [1.6.0](https://github.com/PeterMosmans/ansible-role-bootstrap/compare/v1.5.0...v1.6.0) (2020-05-09)

### Features

- allow SSH key configuration using user module
  ([ba15fa6](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/ba15fa6fbe6cc30c81825badf0695c797b54570e))
- use nicer labels when looping user-related tasks
  ([5cca6dd](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/5cca6ddeec73eff5ad9a8da784e703dbb528e3bb))

### Bug Fixes

- properly deal with loops and empty sublists
  ([1e46633](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/1e466333325353b2481b74bde0a464f9fbb14cef))
- revert earlier pipefail ansible-lint fix
  ([30048a4](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/30048a4abb6c81d543bcb497dce4caac926f7d58))
- set pipefail option for shell command
  ([d3a2be2](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/d3a2be2006fa34922e5f778d00c34fd2e049a928))
- set timezone using native Ansible module
  ([a61c767](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/a61c767287cfd330ea055840199f01ba8ac8e045))

## [1.5.0](https://github.com/PeterMosmans/ansible-role-bootstrap/compare/v1.4.1...v1.5.0) (2020-04-30)

### Features

- support mounts and update-alternatives
  ([9a4d621](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/9a4d6214954c495efa7cc0e409446f29633d1757))

### [1.4.1](https://github.com/PeterMosmans/ansible-role-bootstrap/compare/v1.4.0...v1.4.1) (2020-04-17)

## 1.4.0 (2020-04-17)

### Features

- add autoclean to update step
  ([f83e27e](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/f83e27e08727fa005dac2fee7160c466e9a63199))
- add installation of third-party packages
  ([a0db8b6](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/a0db8b6627caa779b477c751b59e13ee1cf665f2))

### Bug Fixes

- ensure strings are properly quoted
  ([5bf7129](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/5bf7129ff00a796ba9a52e2b62d55fe6cbfd92b7))
- ensure that strings are properly parsed
  ([0e094a8](https://github.com/PeterMosmans/ansible-role-bootstrap/commit/0e094a881bf71ca16c403a8ba16de5ae2b711895))
