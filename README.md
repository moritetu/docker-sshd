Docker SSHD
===========

Docker SSHD container.

Usage
=====

Build container.

```bash
cd centos7
sudo make run
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
