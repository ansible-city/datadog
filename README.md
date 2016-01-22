# Datadog Integration

Master: [![Build Status](https://travis-ci.org/ansible-city/datadog.svg?branch=master)](https://travis-ci.org/ansible-city/datadog)  
Develop: [![Build Status](https://travis-ci.org/ansible-city/datadog.svg?branch=develop)](https://travis-ci.org/ansible-city/datadog)

* [ansible.cfg](#ansible-cfg)
* [Dependencies](#dependencies)
* [Tags](#tags)
* [Examples](#examples)
* [Variables](#variables)

This role install latest datadog agent and configures it.




## ansible.cfg

This role is designed to work with merge "hash_behaviour". Make sure your
ansible.cfg contains these settings

```INI
[defaults]
hash_behaviour = merge
```




## Dependencies

This role has no dependencies. To install this role add this to your
`roles.yml`

```YAML
---

- name: ansible-city.datadog
  version: v1.0
```

and run `ansible-galaxy install -p . -r roles.yml`




## Tags

This role uses two tags: **build** and **configure**

* `build` - Installs Kafka server and all it's dependencies.
* `configure` - Configure and ensures that the Kafka service is running.




## Examples

```YAML
- name: Install datadog agent
  hosts: sandbox

  pre_tasks:
    - name: Update apt
      become: yes
      apt:
        cache_valid_time: 1800
        update_cache: yes
      tags:
        - build

  roles:
    - name: ansible-city.datadog
      datadog:
        tags:
          - role: my_service
          - environment: dev
```




## Variables

### datadog.api_key

API Key.

### datadog.enabled

Set to "no" if you want to stop existing agent.

### datadog.dd_url

default value set to: https://app.datadoghq.com.

### datadog.tags

List of machine tags.
