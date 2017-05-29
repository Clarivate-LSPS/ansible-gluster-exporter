
William-Yeh.gluster_exporter for Ansible Galaxy
============

[![Circle CI](https://circleci.com/gh/Clarivate-LSPS/ansible-gluster-exporter.svg?style=shield)](https://circleci.com/gh/Clarivate-LSPS/ansible-gluster-exporter) [![Build Status](https://travis-ci.org/Clarivate-LSPS/ansible-gluster-exporter.svg?branch=master)](https://travis-ci.org/Clarivate-LSPS/ansible-gluster-exporter)



## Summary

Role for Prometheus [gluster_exporter](https://github.com/ofesseler/gluster_exporter) based on **[William-Yeh.consul_exporter](https://github.com/William-Yeh/ansible-consul-exporter)**

This Ansible role has the following features for [gluster_exporter](https://github.com/ofesseler/gluster_exporter) (a [GlusterFS](https://www.gluster.org/) metrics exporter for [Prometheus](http://prometheus.io/)):

 - Install specific versions of gluster_exporter;
 - Install by compiling from the *master* repo;
 - Handlers for restart/reload/stop events.


## Role Variables


### Mandatory variables

None.


### Optional variables: version

Install specific version of Gluster exporter:

```yaml
# default version
prometheus_gluster_exporter_version: 0.2.7
```

Or, you can optionally download/compile from the *master* branch of gluster_exporter by setting the respective version to `git`:

```yaml
prometheus_gluster_exporter_version: git
```

It will install a temporary Golang compiler in the `prometheus_workdir` directory (defined in `defaults/main.yml`). If you'd like to force rebuild each time, enable the following variable (default is `false`):

```yaml
prometheus_rebuild: true
```


### Optional variables: command-line arguments


Additional command-line arguments, if any (use `gluster_exporter --help` to see the full list of arguments):

```yaml
prometheus_gluster_exporter_opts
```


### Optional variables: use systemd or not

If the Linux distributions are equipped with systemd, this role will use this mechanism accordingly. You can disable this (i.e., use traditional SysV-style init script) by defining the variable to false: `prometheus_gluster_exporter_use_systemd: false`.

```yaml
prometheus_gluster_exporter_use_systemd
```


### Optional variables: general settings of Prometheus

This section lists all variables common for all Prometheus servers and exporters. You may have seen them in my **[williamyeh.prometheus](https://github.com/William-Yeh/ansible-prometheus)** role.


User-configurable defaults:

```yaml
# user and group
prometheus_user:   prometheus
prometheus_group:  prometheus


# directory for executable files
prometheus_install_path:   /opt/prometheus

# directory for logs
prometheus_log_path:       /var/log/prometheus

# directory for PID files
prometheus_pid_path:       /var/run/prometheus



# directory for temporary files
prometheus_download_path:  /tmp


# version of helper utility "gosu"
gosu_version:  1.10
```



## Handlers

- `restart gluster_exporter`

- `reload gluster_exporter`

- `stop gluster_exporter`


## Usage


### Step 1: add role

Add role name `Clarivate-LSPS.gluster_exporter` to your playbook file.


### Step 2: add variables

Set vars in your playbook file, if necessary.

Simple example:

```yaml
---
# file: simple-playbook.yml

- hosts: all
  become: True
  roles:
    - Clarivate-LSPS.gluster_exporter

  vars:

    prometheus_gluster_exporter_opts: "-log.level=debug"
```



## Dependencies

None.


## License

MIT License. See the [LICENSE file](LICENSE) for details.
