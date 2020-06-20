# Ansible Role: awscli

Ansible role for installing an AWS CLI (`awscli`) into a Python3 VirtualEnv.

[![Build Status](https://www.travis-ci.org/PyratLabs/ansible-role-awscli.svg?branch=master)](https://www.travis-ci.org/PyratLabs/ansible-role-awscli)

## Requirements

This role has been tested on Ansible 2.7.0+ against the following Linux Distributions:

  - Amazon Linux 2
  - CentOS 8
  - CentOS 7
  - Debian 10
  - Fedora 29
  - Fedora 30
  - Fedora 31
  - Ubuntu 18.04 LTS

## Disclaimer

If you have any problems please create a GitHub issue, I maintain this role in
my spare time so I cannot promise a speedy fix delivery.

## Role Variables


| Variable                         | Description                                                                   | Default Value        |
|----------------------------------|-------------------------------------------------------------------------------|----------------------|
| `awscli_version`                 | Use a specific version of awscli, eg. `1.16.309`. Specify `false` for latest. | `false`              |
| `awscli_install_dir`             | Installation directory to put awscli virtual environments.                    | `$HOME/.virtualenvs` |
| `awscli_current_dirname`         | Name for the currently active awscli Virtualenv.                              | awscli               |
| `awscli_venv_site_packages`      | Allow venv to inherit packages from global site-packages.                     | `false`              |
| `awscli_install_venv_helper`     | Install a venv helper to launch venv executables from a "bin" directory.      | `true`               |
| `awscli_bin_dir`                 | "bin" directory to install venv-helpers to.                                   | `$HOME/bin`          |
| `awscli_install_os_dependencies` | Allow role to install OS dependencies.                                        | `false`              |
| `awscli_python3_path`            | Specify a path to a specific python version to use in virtualenv.             | _NULL_               |

## Dependencies

No dependencies on other roles.

## Example Playbook

Example playbook for installing to single user:

```yaml
- hosts: awscli_hosts
  roles:
     - { role: xanmanning.awscli, awscli_version: 1.16.309 }
```

Example playbook for installing the latest awscli version globally:

```yaml
---
- hosts: awscli_hosts
  become: true
  vars:
    awscli_install_os_dependencies: true
    awscli_install_dir: /opt/awscli/bin
    awscli_bin_dir: /usr/bin
    awscli_current_dirname: current
  roles:
    - role: xanmanning.awscli
```

### Activating the awscli venv

You need to activate the python3 virtual environment to be able to access `az`.
This is done as per the below:

```bash
source {{ awscli_install_dir }}/{{ awscli_current_dirname }}/bin/activate
```

In the above example global installation playbook, this would look like the
following:

```bash
source /opt/awscli/bin/current/bin/activate
```

## License

[BSD 3-clause](LICENSE.txt)

## Author Information

[Xan Manning](https://xanmanning.co.uk/)
