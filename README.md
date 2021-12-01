Role Name: Victoriamertics vmalert
=========

Deploy and configure [vmalert](https://docs.victoriametrics.com/vmalert.html)

Requirements
------------

Ansible 2.10

Role Variables
--------------

Name | Default Value | Description
---|---|---
`vmalert_version` | 1.69.0 | current version
`vmalert_system_user` | "vmalert" |
`vmalert_system_group` | "vmalert" | 
`vmalert_config_dir` | "/etc/vmalert" | empty
`vmalert_rule_dir` | "/var/lib/vmalert" | 
`vmalert_install_dir` | "/usr/local/bin" | 
`vmalert_repo_dir` | "/var/tmp/archive" | 
`vmalert_remote_write_url` | "http://127.0.0.1:8428" | victoriametrics tsdb
`vmalert_datasource_url` | "http://127.0.0.1:8428" | victoriametrics tsdb
`vmalert_remote_read_url` | "http://127.0.0.1:8428" | victoriametrics tsdb
`vmalert_evaluation_interval` | "1m" |
`vmalert_notifier_url` | "http://127.0.0.1:9093" | prometheus alertmanager


Read this [https://docs.victoriametrics.com/#environment-variables](https://docs.victoriametrics.com/#environment-variables) аnd set more vars, put it into `templates/vmalert.j2`

```sh
mkdir -p /var/tmp/archive
cd /var/tmp/archive
wget https://github.com/VictoriaMetrics/VictoriaMetrics/releases/download/v1.69.0/vmutils-amd64-v1.69.0.tar.gz
```

Example Playbook
----------------

```yaml
---
- hosts: vmdb
  gather_facts: true
  connection: ssh
  roles:
    - v98765_vmalert
```
License
-------

BSD
