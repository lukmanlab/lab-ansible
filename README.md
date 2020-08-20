# CATATAN

- Tools latihan menulis YAML: https://yaml-online-parser.appspot.com/

## Tahapan

### Create VM menggunakan Vagrant
```
vagrant up
```

### Membuat Inventory Host

```
nano hosts
```

```
server1 ansible_host=192.168.99.11 ansible_user=vagrant ansible_ssh_port=22
server2 ansible_host=xxx.173.66.xxx ansible_user=root ansible_ssh_port=2222
```

Copy Public-Key SSH to Server untuk SSH tanpa Password:
```
ssh-copy-id vagrant@192.168.99.11
ssh-copy-id root@xxx.173.66.xxx
```

Testing Login
```
ssh vagrant@192.168.99.11
ssh root@xxx.173.66.xxx
```

Test Ad-Hoc Command, module `ping`:
```
ansible all -i hosts -m ping
```

Result:
```
server1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
server2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

### Ad-Hoc Command
Ketika kita run `ansible all -i hosts -m ping`, ini sudah termasuk Ad-Hoc command.

- Contoh: Ad-Hoc Command update system:
```
ansible all -i hosts -m shell -a "sudo apt update"
```

- Contoh: Ad-Hoc Command install package:
```
ansible all -i hosts -m apt -a "name=zip state=latest" -b
```

## Study Case
1. Gathering Fact Informasi System kedalam File hwreport.txt: [YAML](01-gather_info.yaml)
2. Create Multiple Users, Groups and Assign the Users to Groups: [YAML](01-create_users_groups.yaml)


