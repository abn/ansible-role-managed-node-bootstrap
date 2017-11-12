Managed Node Bootstrap
======================
[![Build Status](https://travis-ci.org/abn/ansible-role-managed-node-bootstrap.svg?branch=master)](https://travis-ci.org/abn/ansible-role-managed-node-bootstrap) [![Ansible Role](https://img.shields.io/ansible/role/21884.svg)](https://galaxy.ansible.com/abn/managed-node-bootstrap/)

Bootstrap an ansible managed node with minimal dependencies. This was originally written to bootstrap instances of distribution base docker images, and hence might require improvements before it becomes stable for non container usage.

Current supported distributions are;
1. Alpine Linux
2. Debian based distributions using apt-get (Ubuntu)
3. OpenSUSE
4. Red Hat based distributions using dnf/yum (Red Hat Enterprise Linux, CentOS, Fedora)

Requirements
------------

No additional requirements are enforced other than an Ansbile version that supports the `raw` module. Development was done on Ansible 2.2+.

Role Variables
--------------

This role supports the following configurations via variables.

1. `managed_node_bootstrap_use_sudo`: Set this to `yes` if the host in question has `sudo` installed and you are connecting as a non-root user.
2. `managed_node_bootstrap_cmd_prefix`: This defaults to `sudo` if `managed_node_bootstrap_use_sudo` is set. You can override this to ensure this prefix is added to all executed commands.
1. `managed_node_bootstrap_done_file`: This specifies which file to use as an indicator if the bootstrap task was successfully executed before.
2. `managed_node_packages_{alpine,debian,opensuse,redhat}`: This is used to configure the list of packages to install for each of these distribution families.

Dependencies
------------

No Dependencies rquired other than Ansible itself.

Example Playbook
----------------

Here is an example play that can be used to bootstrap all your hosts in your inventory. Note that ansible connection method etc. has to be configured external to this. Additionally, note that this requires connecting as a root user, since we assume `sudo` is not available on these instances (docker image assumption). See above for how to alter this behaviour.

    ---
    - name: bootstrap ansible managed node
      hosts: all
      gather_facts: False
      roles:
        - abn.molecule-node-bootstrap

Testing
-------
Before testing, you need to ensure that the submodules required have been cloned.
```sh
git submodule update --init --recursive
```

### Local Environment
This role uses [Molecule](https://molecule.readthedocs.io/en/latest/) and docker instances to enable testing. You can run this locally on your development environment provided you have python installed and are running the docker daemon.

```sh
# install molecule and docker-py requirements
pip install -r test-requirements.txt
molecule test
```

This will as configured in the default molecule scenario, spin up containers of the supported distributions and execute a sample playbook.

### Tox
This project also has [tox](http://tox.readthedocs.io/en/latest/) configured to run against multiple ansible versions with [Molecule](https://molecule.readthedocs.io/en/latest/). This can simply be run using tox.

```sh
tox
```

Refer to the [Molecule documentation](https://molecule.readthedocs.io/en/latest/testing.html) and [tox documentation](http://tox.readthedocs.io/en/latest/) for advance usage instructions.


License
-------

Apache License 2.0
