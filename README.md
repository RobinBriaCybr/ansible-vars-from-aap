# ansible-extra-vars-from-aap

## Example 1: extra_vars
Put this in the extra vars of your template.
```yml
---
conjur_account: "conjur"
conjur_appliance_url: "https://tenant.secretsmgr.cyberark.cloud/api"
conjur_authn_login: "host/data/my_ansible_app"
conjur_authn_api_key: "<secret>"
var_from_extra_vars: "{{ lookup('cyberark.conjur.conjur_variable', 'data/vault/my_safe/my_secret/username', validate_certs=false) }}"
```
Run the playbook `extra_vars.yml`

## Example 2: ssh_connection
Put this in the inventory vars of your target. 
```yml
---
ansible_user: "{{ lookup('cyberark.conjur.conjur_variable', 'data/vault/my_safe/my_secret/username', validate_certs=false) }}"
ansible_ssh_private_key_file: "{{ lookup('cyberark.conjur.conjur_variable', 'data/vault/my_safe/my_secret/password', validate_certs=false, as_file=true) }}"
```

Put this in the extra vars of your template.
```yml
---
conjur_account: "conjur"
conjur_appliance_url: "https://tenant.secretsmgr.cyberark.cloud/api"
conjur_authn_login: "host/data/my_ansible_app"
conjur_authn_api_key: "<secret>"
```

Run the playbook `ssh_connection.yml`

## Example 3: ssh_connection
Put this in the inventory vars of your target. Run the playbook `ssh_connection.yml`
```yml
---
ansible_user: "{{ lookup('cyberark.conjur.conjur_variable', 'data/vault/my_safe/my_secret/username', validate_certs=false) }}"
ansible_ssh_private_key_file: "{{ lookup('cyberark.conjur.conjur_variable', 'data/vault/my_safe/my_secret/password', validate_certs=false, as_file=true) }}"
```

Put this in the extra vars of your template.
```yml
---
conjur_account: "conjur"
conjur_appliance_url: "https://tenant.secretsmgr.cyberark.cloud/api"
conjur_authn_login: "host/data/my_ansible_app"
conjur_authn_api_key: "<secret>"

conjur_path_prefix: "data/vault/my_safe/my_prefix"
conjur_path_suffix: "my_suffix"
```

Run the playbook `ssh_connection_dynamic.yml`
