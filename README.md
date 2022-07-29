# ace-box-ext-template

The `ace-box-ext-template` provides a template structure and examples of how to create a custom [ACE-Box](https://github.com/Dynatrace/ace-box) use case.
## Repository structure

It's important that your external use case complies to a specific folder structure. Most importantly, a folder `roles` need to be available at the repository root that includes at least a `my-use-case` (literal, not renamed) folder.

This `roles` folder and all of it's contents are synced with the ACE-Box's Ansible workdir. Ansible is used to provision use cases including external ones. Upon a successful content sync, Ansible tries to use this `my-use-case` folder as an Ansible role.

An Ansible role is expected to have the following structure:

```
roles/
  my-use-case/
    defaults/
      main.yml
    tasks/
      main.yml
    ...
```

For more information, please see the [official Ansible documentation](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html).

The `my-use-case` role can itself source other Ansible roles. Such roles can either be provided as part of the external repository or included from the ACE-Box default roles. A list of ACE-Box roles can be found [here](https://github.com/Dynatrace/ace-box#curated-roles). Please also see the `examples_roles` folder for examples.

## Variable override (optional)

All default variables can be overriden for an external use case. This can happen in two ways:
- A `defaults/main.yml` is created and added to the respective role directory (e.g. `roles/jenkins/defaults/main.yml`). All external role directories and files are synced with the ACE-Box. The external `main.yml` file would therefore override any ACE-Box default `main.yml`. Attention: This requires that all values in the original `main.yml` are also set in the external `main.yml`.
- A `ace-ext.config.yml` file is added to the repo root. All variables within this file will override the variables set by the ACE-Box. E.g. `dashboard_password: "supersecret"` will override the default `dashboard_password` set by the ACE-Box.
