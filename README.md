# ANSIBLE ROLE: PROMETHEUS

An Ansible role to install Prometheus monitoring system on various platforms.

_**Note:** At the moment, Docker is the only platform supported by this role._

## REQUIREMENTS

* Docker >= 1.12.4

## INSTALLATION

#### USING _ANSIBLE GALAXY_:

```
ansible-galaxy install erjac77.prometheus
```

#### USING _GIT CLONE_:

Clone this repository inside the `roles/` subdirectory of your playbook or inside one of the additional directories specified by the `roles_path` setting in `ansible.cfg`.

```
git clone https://github.com/erjac77/ansible-role-prometheus.git erjac77.prometheus
```

## ROLE VARIABLES

```
---

# Prometheus host platform
prometheus_platform: Docker
#prometheus_platform: "{{ ansible_os_family }}"

# Prometheus application general settings
prometheus_hostname: "{{ hostvars[inventory_hostname]['ansible_default_ipv4']['address'] }}"
prometheus_port: 9090

# Prometheus connection timeout settings
prometheus_connection_retries: 60
prometheus_connection_delay: 5

######### Prometheus configuration parameters ##########
prometheus_scrape_interval: 15s
prometheus_scrape_timeout: 10s
prometheus_evaluation_interval: 30s
prometheus_external_labels: []
prometheus_rule_files: []
prometheus_scrape_configs:
- job_name: prometheus
  scrape_interval: 10s
  scrape_timeout: 10s
  static_configs:
  - targets:
    - "{{ prometheus_hostname }}:{{ prometheus_port }}"
########/ Prometheus configuration parameters ##########
```

### DOCKER VARIABLES

```
---

# Prometheus Docker container settings
prometheus_container_name: prometheus
prometheus_container_image: prom/prometheus
prometheus_container_port: 9090
prometheus_container_data_volume: prometheus-data
```

## DEPENDENCIES

* [ansible-role-docker](https://github.com/erjac77/ansible-role-docker)

## EXAMPLE PLAYBOOK

```
---

- name: Install Prometheus on Docker
  hosts: localhost
  become: yes

  roles:
    - erjac77.prometheus
```

## LICENSE

Apache 2.0

## AUTHOR INFORMATION

Eric Jacob ([@erjac77](https://github.com/erjac77))