Docker SSHD
===========

Docker SSHD container.

## Usage


Build and run sshd container.

```bash
cd centos7
sudo make run
```

Build and run container with sshd running under systemd.

```bash
cd centos7
sudo make runp
```

Login the container with password authentication.

```bash
ssh -p 10022 root@localhost
```

If host keys changed, update keys.

``` bash
ssh-keygen -R "[localhost]:10022"
# or
make update-key
```

Stop and remove container.

```bash
sudo make clean
```

## Test Ansible

```bash
$ cd examples/ansible
$ ansible -i hosts localhost -m ping
localhost | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```