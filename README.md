# ansible-users

This role has a few groups defined as variables:
- service_users
- sre_users
- ms_users
- dev_users
- ps_users
- flex_solutions_users
- solutions_users
- se_users

This role creates all enabled users and _deletes_ all users that are not enabled. By default the service, sre and ms users are enabled.
To change the defaults:

* when running `ansible-playbook` and changing the groups adhoc, use the json/yaml notation. This is *very* important - if you use the usual `-e sre_users_enabled=false` notation, `sre_users_enabled` will actually be _true_!

```
  STACK_NAME=zonetvstg ansible-playbook -i $(which ansible-inventory-azure) -e '{ ps_users_enabled: true }' add-users.yml
```

* when changing those in a playbook

```
- hosts: all
  any_errors_fatal: true
  become: yes
  gather_facts: yes
  roles:
    - { role: users,
        ps_users_enabled: true
      }
```

* when building a new image using packer

```
{
  "type": "ansible-local",
  "playbook_dir": ".",
  "playbook_file": "run.yml",
  "extra_arguments": ["-e", "'{ aws_region: us-east-1, ms_users_enabled: false, dev_users_enabled: true }'"]
},
```
