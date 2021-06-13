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
`vmalert_version` | 1.61.1 | current version
`vmalert_system_user` | "vmalert" |
`vmalert_system_group` | "vmalert" | 
`vmalert_config_dir` | "/etc/vmalert" | 
`vmalert_install_dir` | "/usr/local/bin" | 
`vmalert_repo_dir` | "/var/tmp/archive" | 
`vmalert_remoteWrite_url` | "http://127.0.0.1:8428" | victoriametrics tsdb
`vmalert_datasource_url` | "http://127.0.0.1:8428" | victoriametrics tsdb
`vmalert_remoteRead_url` | "http://127.0.0.1:8428" | victoriametrics tsdb
`vmalert_evaluationInterval` | "1m" |
`vmalert_rule` | "{{ vmalert_config_dir }}/*.yaml" | rules
`vmalert_notifier_url` | "http://127.0.0.1:9093" | prometheus alertmanager


Read this [https://docs.victoriametrics.com/#environment-variables](https://docs.victoriametrics.com/#environment-variables) аnd set more vars, put it into `templates/vmalert.j2`

```sh
mkdir -p /var/tmp/archive
cd /var/tmp/archive
wget https://github.com/VictoriaMetrics/VictoriaMetrics/releases/download/v1.57.1/vmutils-amd64-v1.61.1.tar.gz
```

Example Playbook
----------------

```yaml
---
- hosts: exporters
  gather_facts: true
  connection: ssh
  roles:
    - v98765_vmalert

  tasks:
    - name: copy vmalert targets
      copy:
        src: "{{ item }}"
        dest: "{{ vmalert_config_dir }}/"
        force: true
        owner: root
        group: vmalert
        mode: 0644
      with_fileglob: "{{ vmalert_rules_files }}"
      tags:
        - vmalert_configure
```
host_vars/exporters.yml
```yaml
vmalert_rules_files:
  - rules/*.yaml
```
License
-------

BSD
