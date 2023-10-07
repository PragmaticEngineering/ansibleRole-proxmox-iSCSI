proxmox_iscsi
=========
This role updates your iSCSI configuration on the proxmox nodes according to the multipath recommendations. It is important to start all required iSCSI connections at boot time. You can do this by setting 'node.startup' to 'automatic'.

The default 'node.session.timeo.replacement_timeout' is 120 seconds. We recommend using a much smaller value of 15 seconds instead.

You can set those values in '/etc/iscsi/iscsid.conf' (defaults). If you are already connected to the iSCSI target, you need to modify the target specific defaults in '/etc/iscsi/nodes/<TARGET>/<PORTAL>/default'.

A modified 'iscsid.conf' file contains the following lines:
```
node.startup = automatic
node.session.timeo.replacement_timeout = 15
```

Please configure your iSCSI storage on the GUI if you have not done that already ("Datacenter/Storage: Add iSCSI target").

Requirements
------------

none

Role Variables
--------------

none

Dependencies
------------

none

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```yaml

- name: proxmox_iscsi.yml
  hosts: proxmox-01.home.local
  gather_facts: true
  vars_prompt: 
  - name: "ansible_password"
    prompt: "Enter the remote password"
    private: yes
  vars: 
    ansible_user: root
  tasks:
  - import_role: 
      name: proxmox/iscsi
```

License
-------

GNU GPLv3
