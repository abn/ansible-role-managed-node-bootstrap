Managed Node Bootstrap
======================

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

Here is an example play that can be used to bootstrap all your hosts in your inventory. Note that ansible connection method etc. has to be configured external to this. Additionally, note that this requires connecting as a root user, since we assume `sudo` is not available on these instances (docker image assumption). See above for how to alter this behavior.

    ---
    - name: bootstrap ansible managed node
      hosts: all
      gather_facts: False
      roles:
        - abn.molecule-node-bootstrap


License
-------

Apache License 2.0
