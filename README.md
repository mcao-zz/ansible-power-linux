<!-- This should be the location of the title of the repository, normally the short name -->
# IBM Power Systems Linux Collection

<!-- Build Status, is a great thing to have at the top of your repository, it shows that you take your CI/CD as first class citizens -->
<!-- [![Build Status](https://travis-ci.org/jjasghar/ibm-cloud-cli.svg?branch=master)](https://travis-ci.org/jjasghar/ibm-cloud-cli) -->

<!-- Not always needed, but a scope helps the user understand in a short sentence like below, why this repo exists -->
## Scope

The **IBM Power Systems Linux Automation** a a central place to provide modules that support Linux
automation on Power. The content here helps manage workloads on Power infrastructure as part of your
wider enterprise automation strategy.


The **IBM Power Systems Linux Automation*** is currently supported via


Currently the Linux modules validated on Power systesm including Ansible.Posix collection.
 It is a collection written by the Ansible Core Team.  More information can be found at

Ansible.Posix
https://docs.ansible.com/ansible/latest/collections/ansible/posix/index.html


## Ansible

- Requires Ansible 2.9 or newer
- For help installing Ansible, refer to the [Installing Ansible] section of the Ansible Documentation
- Requires Python 2.7 or newer

## Resources

Documentation of modules is generated on [GitHub Pages][pages].


## Examples

### Build kernel  ( see install_kernel.yaml for full kernel install and build playbook )
- name: apply optional patch file(s)
  shell: "git apply {{ item }}"
  with_items: "{{ patch_files.files | map(attribute='path') | list }}"
  when: patches is defined or all patches is defined
  args:
    chdir: /tmp/kernel-download

- name: install kernel
  shell: "{{ item }}"
  with_items:
  - make olddefconfig
  - make -j 20
  - make modules
  - make modules_install
  - make install
  register: out
  args:
    chdir: /tmp/kernel-download


### Example  SELinux

selinux – Change policy and state of SELinux

- name: Enable SELinux
  selinux:
    policy: targeted
    state: enforcing

- name: Put SELinux in permissive mode, logging actions that would be blocked.
  selinux:
    policy: targeted
    state: permissive

- name: Disable SELinux
  selinux:
    state: disabled


Call this playbook as selinux_setting.yml.  In order to get this playbook to work, you
should have the  ansible-collection-ansible-posix package installed.

$ sudo dnf install ansible-collection-ansible-posix

Then you can run the playbook with ansible-playbook command.

$ ansible-playbook selinux_enforcing.yml

## License & Authors

If you would like to see the detailed LICENSE click [here](LICENSE).

```text
Copyright:: 2021- IBM, Inc

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
```

Authors:
- Mingming Cao <Mingming.cao@ibm.com>
