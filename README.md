# cockroach-ansible

### How to use

```bash
ansible-playbook -i inventory/db-servers.ini cockroachDB.yaml  --become --become-method=sudo -t preinstall
```

```
ansible-playbook -i inventory/db-servers.ini cockroachDB.yaml  --become --become-method=sudo -t cockroach-manual
```

```
ansible-playbook -i inventory/db-servers.ini cockroachDB.yaml  --become --become-method=sudo -t cockroach_systemd
```