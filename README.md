# Install:

$ python3 -m pip install --user ansible

`Inventory.ini`:

ubuntu@ip

## Pass less authentication:

### Using **SSH**:

`ssh-keygen`

`ssh-copy-id -f "-o IdentityFile <.pem>" ubuntu@ip`

### Using **Pass**:
 Update sshd_config to yes for pass

`sudo passwd ubuntu`

`sudo systemctl restart ssh`


## Adhoc Commands:

`ansible -i inventory.ini -m ping all/app/db<group>`

-m : module
-i: inventory file
-a : Argument

`ansible -i inventory.ini -m "shell" -a "apt update" all/app/db<group>`

## Run a Playbook:

`ansible-playbook -i inventory.ini <playbook.yaml>`

### Playbook Format:

```
hosts:
remote-user:
tasks:
    - module

    - module
```

### Sample:

```
---

- hosts: all

  become: true

  tasks:

    - name: Install apache httpd

      ansible.builtin.apt:

        name: apache2

        state: absent

        update_cache: yes

    - name: Copy file to remote server

      ansible.builtin.copy:

        src: index.html

        dest: /var/www/html/index.html

        owner: root

        group: root

        mode: '0644'
```