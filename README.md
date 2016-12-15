Role Name
=========

Use Ansible to configure RaspberryPis to be dashboards.

Requirements
------------

- Download [The latest Raspbian release](https://www.raspberrypi.org/downloads/raspbian/) (make sure it includes the PIXEL desktop)
- Follow the [installation guide](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)
- Start up your Pi and find out the IP address
- Optionally, use `raspi-config` to set the hostname of your Pi to save you having to use IP addresses for provisioning

Role Variables
--------------

### Group Vars

`dashboard_url` The URL to launch and display on the Pi on boot

Should be defined for each host.

Defined outside of this repo to allow you to keep a list of your dashboards in your project repo or somewhere not public.

Example Playbook
----------------

```yaml
- hosts: dashboards
  roles:
    - pi-dashboard
```
