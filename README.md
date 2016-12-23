# Ansible role: dhcpd
Installs and configures DHCP server.

## Requirements
None.

## Role Variables
|Key|Type|Description|Default|
|:--|:---|:----------|:------|
|dhcpd_bind_interface|String||eth0|
|dhcpd_domain_name|String||localhost|
|dhcpd_domain_name_servers|String||8.8.8.8|
|dhcpd_default_lease_time|Integer||600|
|dhcpd_max_lease_time|Integer||7200|
|`dhcpd_subnets`|Array||[]|
|`dhcpd_groups`|Array||[]|

#### dhcpd_subnets
|Key|Type|Description|
|:--|:---|:----------|
|subnet|String||
|routers|String||
|netmask|String||
|next_server|String||
|range|String||
|options|Hash||

#### dhcpd_groups
|Key|Type|Description|
|:--|:---|:----------|
|next_server|String||
|filename|String||
|`hosts`|Hash||

#### hosts
`key` is host identifier.

|Value|Type|Description|
|:--|:---|:----------|
|address|String|MAC address|

## Dependencies
None.

## Example playbook

```yaml
- hosts: all
  roles:
    - { role: dhcpd }
  vars:
    dhcpd_bind_interface: enp0s8
    dhcpd_subnets:
      - subnet: 192.168.33.0
        routers: 192.168.33.1
        netmask: 255.255.255.0
        next_server: 192.168.33.1
        range: "192.168.33.240 192.168.33.250"
    dhcpd_groups:
      - filename: pxelinux.0
        hosts:
          host1:
            address: 00:11:AA:BB:CC:DD
          host2:
            address: 11:22:CC:DD:EE:EE      
```
