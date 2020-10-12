## Tearing Down The Environment

Before our last (fictional) Ansible Tower administrator left, they were unable to complete a teardown script to clean out the Ansible Tower environment prior to the Tower server being decommissioned. Our first task as the new Ansible Tower administrator will be to complete this task. Since we have created several assets in our Ansible Tower environment, we can use our Ansible Tower server to test our teardown script.

All modules that build assets have a `state` option. By default, the state option is ‘present’ which means the assets need to exist in Ansible Tower in the specified state. Since all of our examples so far have created things, we did not need to include the `state` parameter. The opposite value to remove an asset from Tower is `state: absent`. So, for example, to delete the ops user you would need a task like:

```yml
    - name: Delete ops user
      tower_user:
        username: "ops"
        state: absent
```

There was an email that was found with some details about the teardown script; below is the recovered contents. Create a new file called `clean_tower.yml` with its contents:

```yml
---
- name: Remove lab assets
  hosts: localhost
  connection: local
  gather_facts: False
  collections:
    - awx.awx

  tasks:
    - name: Remove workflow job templates
      tower_workflow_job_template:
        state: absent
        name: "{{ item.id }}"
      loop: "{{ lookup('awx.awx.tower_api', 'workflow_job_templates', return_all=True, wantlist=True) }}"
      loop_control:
        label: "{{ item.name }}"

    - name: Remove job templates
      tower_job_template:
        state: absent
        name: "{{ item.id }}"
      loop: "{{ lookup('awx.awx.tower_api', 'job_templates', return_all=True, wantlist=True) }}"
      loop_control:
        label: "{{ item.name }}"

    - name: Remove projects
      tower_project:
        state: absent
        name: "{{ item.id }}"
      loop: "{{ lookup('awx.awx.tower_api', 'projects', return_all=True, wantlist=True) }}"
      loop_control:
        label: "{{ item.name }}"

    - name: Remove Inventories
      tower_inventory:
        state: absent
        name: "{{ item.id }}"
        organization: "{{ item.organization }}"
      loop: "{{ lookup('awx.awx.tower_api', 'inventories', return_all=True, wantlist=True) }}"
      loop_control:
        label: "{{ item.name }}"

    - name: Remove Credentials
      tower_credential:
        state: absent
        name: "{{ item.id }}"
        credential_type: "{{ item.credential_type }}"
      loop: "{{ lookup('awx.awx.tower_api', 'credentials', return_all=True, wantlist=True) }}"
      loop_control:
        label: "{{ item.name }}"
```

Start by running this script and then see what kind of assets are left. Using the example code above, create additional tasks to remove the remaining Organizations and users. Your new boss will be extra happy if you can also set the login message to “This instance is being retired” (refer to the first lab example for how to do that).
