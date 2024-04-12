# Cockroach-Ansible

This repository hosts an Ansible playbook designed for the seamless deployment and management of CockroachDB clusters on Ubuntu 22.04 LTS environments. It requires a private network configuration between the servers to ensure secure and efficient communication.

### Architecture Overview

                                        +------------------+
                                        |  Client Access   |
                                        +--------+---------+
                                                 |
                                                 |
                                        +--------v--------+
                                        |   HAProxy       |
                                        | (Load Balancer) |
                                        +--------+--------+
                                                 |
                                                 |
                            +--------------------+---------------------+
                            |                    |                     |
                            |                    |                     |
                            v                    v                     v
                    +-------+--------+   +-------+--------+    +-------+--------+
                    |  Server 1      |   |  Server 2      |    |  Server 3      |
                    |  (CockroachDB) |   |  (CockroachDB) |    |  (CockroachDB) |
                    |  IP: 10.0.1.1  |   |  IP: 10.0.1.2  |    |  IP: 10.0.1.3  |
                    +-------+--------+   +-------+--------+    +-------+--------+


## Repository Overview

**Note:** Ensure that you are operating within a private network setup to utilize this playbook effectively.

### How to Use This Playbook

1. **Configuration Review**: Begin by examining the `inventory/group_vars/all.yaml` and `inventory/db-servers.ini` files.
2. **Customize Variables**: Modify the variables in the aforementioned files to tailor the setup to your specific requirements.

### Step-by-Step Guide to Deploy CockroachDB

- **Prepare Servers**: Ready your servers for the CockroachDB installation by executing the following command:
  ```bash
  ansible-playbook -i inventory/db-servers.ini cockroachDB.yaml --become --become-method=sudo -t preinstall
  ```

- **Manual Cluster Installation**: To install the CockroachDB cluster manually:
  ```
  ansible-playbook -i inventory/db-servers.ini cockroachDB.yaml --become --become-method=sudo -t cockroach-manual
  ```

- **Systemd Cluster Installation**: For installing the CockroachDB cluster with systemd integration:
  ```
  ansible-playbook -i inventory/db-servers.ini cockroachDB.yaml --become --become-method=sudo -t cockroach_systemd
  ```

- **Install HAProxy**: Set up HAProxy as a load balancer by running:
  ```
  ansible-playbook -i inventory/db-servers.ini cockroachDB.yaml --become --become-method=sudo -t haproxy
  ```

This playbook offers a structured approach to deploying a robust CockroachDB environment, enhancing your database infrastructure with minimal manual intervention.