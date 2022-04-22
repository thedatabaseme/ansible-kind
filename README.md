ansible-kind
=========

This role will help you to setup / install [kind](https://kind.sigs.k8s.io/) on your system.
Also ansible-kind supports you in creating and deleting kind clusters.

Kind is a leightweight solution to run Kubernetes on top of Docker. You can create yourself
a cluster setup with multiple control-planes and / or worker nodes.

Requirements
------------

 - Ansible 2.7 or higher.
 - ansible-kind `install` will only work on Debian OS family (Debian, Ubuntu...) as for now.
   Cluster management will work regardless of which Linux OS family you're using.

All required software for kind will be installed using this role. You don't need to install
software manually. For instance, Docker is needed and will be installed.

Role Variables
--------------

## Optional variables

| Variable Name | Description              | Default value |
|---------------|--------------------------|---------------|
|kind_version |Specify the kind version you want to install (e.g. `v0.12.0` or `v0.10.0`).<br>You can also specify `latest`.|`latest`|
|kind_install_dir|Installation destination for the kind binary|`/usr/local/bin`|
|cluster_name|Specify your kind clustername. Be aware, a cluster name must be unique.|`kind`|
|control_nodes|Number of control-plane nodes that will be created using this role.|`1`|
|worker_nodes|Number of worker nodes that will be created using this role.|`2`|


Dependencies
------------

None.

Example Playbook
----------------

This role works using TAGs to specify if you want to `install` kind, `create` or `delete`
a cluster. You may combine the TAGs as you like, but the combination of `create` and
`delete` makes no sense.

You can find an example playbook in this repository as `ansible-kind.yml`. Here are some
examples in calling this playbook:

    - ansible-playbook ansible-kind.yml -e "HOSTS=vmkind" --tags "install, create" -e "cluster_name=mytestcluster control_nodes=3 worker_nodes=2" -k -K -u <username>

This will install kind in the `latest` version. After the installation, a cluster
`mytestcluster` will be created with 3 control-plane nodes and 2 worker nodes.

License
-------

GPL 3.0

Author Information
------------------

ansible-kind was created by Philip Haberkern (thedatabaseme).

Inspiration in writing this role was `ansible-role-kind` [here](https://github.com/PyratLabs/ansible-role-kind).