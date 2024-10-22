# postgres
ansible playbook для postgres

# протестировано
```
# almalinux 8
ansible_os_family=RedHat
ansible_distribution=AlmaLinux
ansible_distribution_version=8.10

# ubuntu 22.04
ansible_os_family=Debian
ansible_distribution=Ubuntu
ansible_distribution_version=22.04

```

# params
```
env=dev
deploy_user=ubuntu
db_user_name=test
db_name=test
db_user_password: test
db_white_address=127.0.0.1/32
```

## configure
```
listen_addresses='*'
ssl=off
max_connections=20
shared_buffers=256MB
effective_cache_size=768MB
maintenance_work_mem= 64MB
checkpoint_completion_target=0.9
wal_buffers=7864kB
default_statistics_target=100
random_page_cost=1.1
effective_io_concurrency=200
work_mem=6553kB
huge_pages=off
min_wal_size=1GB
max_wal_size=4GB

postgresql_databases=[{'name': "{{ db_name }}"}]
postgresql_users=[{'name': "{{ db_user_name }}", 'password': "{{ db_user_password }}", 'priv': 'ALL', 'db': "{{ db_name }}"}]
postgresql_hba_entries=[{'type': 'local', 'database': 'all', 'user': 'postgres', 'auth_method': 'peer'}, {'type': 'local', 'database': 'all', 'user': 'all', 'auth_method': 'peer'}, {'type': 'host', 'database': "{{ db_name }}", 'user': "{{ db_user_name }}", 'address': "{{ db_white_address }}", 'auth_method': "{{ postgresql_auth_method }}"}, {'type': 'host', 'database': 'all', 'user': 'all', 'address': '127.0.0.1/32', 'auth_method': "{{ postgresql_auth_method }}"}, {'type': 'host', 'database': 'all', 'user': 'all', 'address': '::1/128', 'auth_method': "{{ postgresql_auth_method }}"}]
postgresql_auth_method=scram-sha-256
postgresql_user=postgres
postgresql_locales=['en_US.UTF-8','ru_RU.UTF-8']
```

# to-do
Переделать привилегии https://docs.ansible.com/ansible/latest/collections/community/postgresql/postgresql_privs_module.html#ansible-collections-community-postgresql-postgresql-privs-module
