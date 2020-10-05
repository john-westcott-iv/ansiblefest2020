## Building `devel` Version of Collection

To build the collection from source, we simply use the `make` command with the target `install_collection`. This will eventually run `ansible-galaxy` for installing the collection.

> **Note:** You must have ansible-galaxy 2.9 or later in order for this command to run properly.

First we need to make sure that the `make` command itself is installed in the environment:

```
[student1@ansible-1 awx]$ sudo yum install -y make
Last metadata expiration check: 2:22:55 ago on Sun 20 Sep 2020 07:01:27 PM UTC.
Dependencies resolved.
=============================================================================
 Package  Architecture   Version            Repository                 Size
=============================================================================
Installing:
 make     x86_64         1:4.2.1-10.el8     rhel-8-baseos-rhui-rpms    498 k

Transaction Summary
=============================================================================
Install  1 Package

Total download size: 498 k
Installed size: 1.4 M
Downloading Packages:
make-4.2.1-10.el8.x86_64.rpm                      4.5 MB/s | 498 kB     00:00    
-----------------------------------------------------------------------------
Total                                             2.3 MB/s | 498 kB     00:00     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                    1/1
  Installing       : make-1:4.2.1-10.el8.x86_64                         1/1
  Running scriptlet: make-1:4.2.1-10.el8.x86_64                         1/1
  Verifying        : make-1:4.2.1-10.el8.x86_64                         1/1

Installed:
  make-1:4.2.1-10.el8.x86_64                                                                       

Complete!
```

Once `make` is installed we can install the `devel` version of the collection with the `make` command and the `install_collection` target:

```
[student1@ansible-1 awx]$ make install_collection
ansible-playbook -i localhost, awx_collection/tools/template_galaxy.yml -e collection_package=awx -e collection_namespace=awx -e collection_version=14.1.0 -e '{"awx_template_version":false}'

PLAY [Template the collection galaxy.yml] *********************************************************

TASK [file] *****************************************************************************
ok: [localhost]

TASK [copy] *****************************************************************************
changed: [localhost]

TASK [template_galaxy : Set the collection version in the tower_api.py file] **********************
skipping: [localhost]

TASK [template_galaxy : Set the collection type in the tower_api.py file] *************************
ok: [localhost]

TASK [template_galaxy : Change module doc_fragments to support desired namespace and package names] ***
skipping: [localhost] => (item=tower.py)
skipping: [localhost] => (item=tower_api.py)
skipping: [localhost] => (item=tower_schedule_rrule.py)
skipping: [localhost] => (item=tower_credential.py)
skipping: [localhost] => (item=tower_credential_input_source.py)
skipping: [localhost] => (item=tower_credential_type.py)
skipping: [localhost] => (item=tower_export.py)
skipping: [localhost] => (item=tower_group.py)
skipping: [localhost] => (item=tower_host.py)
skipping: [localhost] => (item=tower_import.py)
skipping: [localhost] => (item=tower_instance_group.py)
skipping: [localhost] => (item=tower_inventory.py)
skipping: [localhost] => (item=tower_inventory_source.py)
skipping: [localhost] => (item=tower_inventory_source_update.py)
skipping: [localhost] => (item=tower_job_cancel.py)
skipping: [localhost] => (item=tower_job_launch.py)
skipping: [localhost] => (item=tower_job_list.py)
skipping: [localhost] => (item=tower_job_template.py)
skipping: [localhost] => (item=tower_job_wait.py)
skipping: [localhost] => (item=tower_label.py)
skipping: [localhost] => (item=tower_license.py)
skipping: [localhost] => (item=tower_meta.py)
skipping: [localhost] => (item=tower_notification_template.py)
skipping: [localhost] => (item=tower_organization.py)
skipping: [localhost] => (item=tower_project.py)
skipping: [localhost] => (item=tower_project_update.py)
skipping: [localhost] => (item=tower_receive.py)
skipping: [localhost] => (item=tower_role.py)
skipping: [localhost] => (item=tower_schedule.py)
skipping: [localhost] => (item=tower_send.py)
skipping: [localhost] => (item=tower_settings.py)
skipping: [localhost] => (item=tower_team.py)
skipping: [localhost] => (item=tower_token.py)
skipping: [localhost] => (item=tower_user.py)
skipping: [localhost] => (item=tower_workflow_job_template.py)
skipping: [localhost] => (item=tower_workflow_job_template_node.py)
skipping: [localhost] => (item=tower_workflow_launch.py)
skipping: [localhost] => (item=tower_workflow_template.py)

TASK [template_galaxy : Change inventory file to support desired namespace and package names] *****
skipping: [localhost]

TASK [template_galaxy : Get sanity tests to work with non-default name] ***************************
skipping: [localhost]

TASK [template_galaxy : Template the galaxy.yml file] *********************************************
changed: [localhost]

TASK [template_galaxy : Template the README.md file] **********************************************
changed: [localhost]

TASK [Make substitutions in source to sync with templates] ****************************************
ok: [localhost]

TASK [Template the galaxy.yml source file (should be commited with your changes)] *****************
ok: [localhost]

TASK [Template the README.md source file (should be commited with your changes)] ******************
changed: [localhost]

PLAY RECAP ******************************************************************************
localhost: ok=8 changed=4 unreachable=0 failed=0 skipped=4 rescued=0 ignored=0   

ansible-galaxy collection build awx_collection_build --force --output-path=awx_collection_build
[WARNING]: Found unknown keys in collection galaxy.yml at
'/home/student1/awx/awx_collection_build/galaxy.yml': build_ignore
Created collection for awx.awx at /home/student1/awx/awx_collection_build/awx-awx-14.1.0.tar.gz
rm -rf ~/.ansible/collections/ansible_collections/awx/awx
ansible-galaxy collection install awx_collection_build/awx-awx-14.1.0.tar.gz
Process install dependency map
Starting collection install process
Installing 'awx.awx:14.1.0' to '/home/student1/.ansible/collections/ansible_collections/awx/awx'
```

This builds the collection and installs it into the `~/.ansible/collections/ansible_collections` directory, making the development version of the collection available to run under Ansible.
