# Ansible

If you use `include_role` / `import_role` from another role, you may expect that the `defaults/main.yml` from the _Parent Role_ get used by the _Child Role_, but it is actually the defaults of each role have a higher precedence than the defaults of a parent role [[Docs]](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#id15). 

So in order to have these sane defaults when making a wrapper role, you have to pass the vars you want to override specifically via "vars:"

## Testing

Run this example by using `ansible-playbook`

```sh
$ ansible-playbook site.yml


PLAY [Failing Example] ***********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************************
ok: [localhost]

TASK [Include Role 1] ************************************************************************************************************************************************************************************

TASK [Include Role 2. This will not override the defaults of role2] **************************************************************************************************************************************

TASK [role2 : Print Variables] ***************************************************************************************************************************************************************************
ok: [localhost] => (item=role2_var) => {
    "msg": "role2_var = role2"
}
ok: [localhost] => (item=role2_var2) => {
    "msg": "role2_var2 = role2"
}
ok: [localhost] => (item=random_var) => {
    "msg": "random_var = role1"
}

TASK [Include Role 2, specify vars to pass. This will fail due to using the same var name.] **************************************************************************************************************

TASK [role2 : Print Variables] ***************************************************************************************************************************************************************************
fatal: [localhost]: FAILED! => {"msg": "An unhandled exception occurred while running the lookup plugin 'vars'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ role2_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: recursive loop detected in template string: {{ role2_var }}"}
...ignoring

PLAY [Working Example] ***********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************************
ok: [localhost]

TASK [Include Role 1] ************************************************************************************************************************************************************************************

TASK [role1-working : Define role2 object vars for use in include_role] **********************************************************************************************************************************
ok: [localhost] => (item=role2_var)

TASK [Include Role 2. This will not override the defaults of role2] **************************************************************************************************************************************

TASK [role2 : Print Variables] ***************************************************************************************************************************************************************************
ok: [localhost] => (item=role2_var) => {
    "msg": "role2_var = role1"
}
ok: [localhost] => (item=role2_var2) => {
    "msg": "role2_var2 = role2"
}
ok: [localhost] => (item=random_var) => {
    "msg": "random_var = role1"
}

TASK [Include Role 2 but prefix role1 default vars] ******************************************************************************************************************************************************

TASK [role2 : Print Variables] ***************************************************************************************************************************************************************************
ok: [localhost] => (item=role2_var) => {
    "msg": "role2_var = role1"
}
ok: [localhost] => (item=role2_var2) => {
    "msg": "role2_var2 = role2"
}
ok: [localhost] => (item=random_var) => {
    "msg": "random_var = role1"
}

PLAY RECAP ***********************************************************************************************************************************************************************************************
localhost                  : ok=7    changed=0    unreachable=0    failed=0   
```