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
server2 ansible_host=202.173.66.126 ansible_user=root ansible_ssh_port=2222
```

Copy Public-Key SSH to Server untuk SSH tanpa Password:
```
ssh-copy-id vagrant@192.168.99.11
ssh-copy-id root@202.173.66.126
```

Testing Login
```
ssh vagrant@192.168.99.11
ssh root@202.173.66.126
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


