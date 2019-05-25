# Ansible

If you use `include_role` / `import_role` from another role, you may expect that the `defaults/main.yml` from the _Parent Role_ get used by the _Child Role_, but it is actually the defaults of each role have a higher precedence than the defaults of a parent role [[Docs]](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#id15). 

So in order to have these sane defaults when making a wrapper role, you have to pass the vars you want to override specifically via "vars:"

## Testing

Run this example by using `ansible-playbook`

```sh
$ ansible-playbook site.yml

PLAY [Failing Examples] **********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************************
ok: [localhost]

TASK [Include Failing Parent Role #1] ********************************************************************************************************************************************************************

TASK [Include the wrapped child-role. This WILL NOT override the defaults of the child role.] ************************************************************************************************************

TASK [child-role : Child Role will print the variables it has received] **********************************************************************************************************************************
ok: [localhost] => (item=child_role_var) => {
    "msg": "child_role_var = this var comes from the child-role defaults/main.yml"
}
ok: [localhost] => (item=child_role_var2) => {
    "msg": "child_role_var2 = this var comes from the child-role defaults/main.yml"
}
ok: [localhost] => (item=parent_role_var) => {
    "msg": "parent_role_var = this var comes from the parent-role defaults/main.yml"
}

TASK [Include the wrapped child-role, specify vars to pass. This will fail due to using the same var name.] **********************************************************************************************

TASK [child-role : Child Role will print the variables it has received] **********************************************************************************************************************************
fatal: [localhost]: FAILED! => {"msg": "An unhandled exception occurred while running the lookup plugin 'vars'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ child_role_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ child_role_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: An unhandled exception occurred while templating '{{ child_role_var }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: recursive loop detected in template string: {{ child_role_var }}"}
...ignoring

PLAY [Working Examples] **********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************************
ok: [localhost]

TASK [Include Success Parent Role #1] ********************************************************************************************************************************************************************

TASK [parent-role-success1 : Define child_role object vars for use in include_role] **********************************************************************************************************************
ok: [localhost] => (item=child_role_var)

TASK [Include child-role. This WILL override the defaults of role2] **************************************************************************************************************************************

TASK [child-role : Child Role will print the variables it has received] **********************************************************************************************************************************
ok: [localhost] => (item=child_role_var) => {
    "msg": "child_role_var = this var comes from the parent-role defaults/main.yml"
}
ok: [localhost] => (item=child_role_var2) => {
    "msg": "child_role_var2 = this var comes from the child-role defaults/main.yml"
}
ok: [localhost] => (item=parent_role_var) => {
    "msg": "parent_role_var = this var comes from the parent-role defaults/main.yml"
}

TASK [Include child-role but use a prefixed parent_role variable] ****************************************************************************************************************************************

TASK [child-role : Child Role will print the variables it has received] **********************************************************************************************************************************
ok: [localhost] => (item=child_role_var) => {
    "msg": "child_role_var = this var comes from the parent-role defaults/main.yml"
}
ok: [localhost] => (item=child_role_var2) => {
    "msg": "child_role_var2 = this var comes from the child-role defaults/main.yml"
}
ok: [localhost] => (item=parent_role_var) => {
    "msg": "parent_role_var = this var comes from the parent-role defaults/main.yml"
}

PLAY RECAP ***********************************************************************************************************************************************************************************************
localhost                  : ok=7    changed=0    unreachable=0    failed=0   
```