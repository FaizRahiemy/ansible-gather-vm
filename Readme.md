Ansible Gather VM Playbook
-------------------------------------------

This is a simple Ansible Playbook to gather VM's IP address, OS name, OS version, and determine whether it compliant to a determined requirements:
* Define Ubuntu 24 as comply, where other OS do not comply.

## Installation
To use this playbook, you need to have Ansible and additionally, netaddr Python library is required to gather VM's private IP address.

    pip install ansible
    pip install netaddr

## How to Use
Before running the playbook, you will need to determine the inventory, this can be achieved by filling out the `hosts` file:

    [all]
    put remote IP address here

After that, you need to determine the SSH key location as well, this is defined on `site.yml`:

    ...
    vars:
        ansible_ssh_private_key_file: "[SSH Key path]"
    ...

Once you fill the hosts file and determine the SSH key location, you can directly run the playbook by running the command below

    ansible-playbook -i hosts site.yml

This playbook will returns:
* VM hostname
* VM private IP address
* VM OS name
* VM OS version
* VM compliance status

Sample result:

    ok: [localhost] => {
        "msg": [
            "hostname: remote-server",
            "ip address: 10.40.112.3",
            "os name: Ubuntu",
            "os version: 22.04",
            "os comply: False"
        ]
    }