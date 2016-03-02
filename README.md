# Before you start

- Download [NOOBS](https://www.raspberrypi.org/downloads/noobs/)
- Follow the [NOOBS setup guide](https://www.raspberrypi.org/help/noobs-setup/)
- When you boot the Pi for the first time, choose to download Raspbian
- Find out the IP address of your fresh Pi, and then use this tool

# Usage

`ansible-playbook -i hosts <GROUP_NAME>.yml`

e.g.

`ansible-playbook -i hosts sport-dax.yml`

This will provision all pi's that are in the `sport-dax` group to dispay the URL specified in the `hosts` file.

# Configuration

### Adding a new group

In the root of the project make a new `<GROUP_NAME>.yml` file, named after your new group, that looks something like this

```yaml
---
- hosts: <GROUP_NAME>
  roles:
    - pi-dashboard

```

e.g.

```yaml
---
- hosts: sport-dax
  roles:
    - pi-dashboard
```

In the `hosts` file, add a new block for your group that looks something like this

```
[<GROUP_NAME>]
<PI_IP_ADDRESS>
[<GROUP_NAME>:vars]
dashboard_url=<URL_TO_DISPLAY>
```

e.g.

```
[sport-dax]
10.10.10.2
[sport-dax:vars]
dashboard_url=http://10.10.36.91:3000/dashboard/db/sport-on-tap
```

### Adding a pi to a group

In the `hosts` file, you can add additional IP addressed under the `[<GROUP_NAME>]`

e.g.

```
[sport-dax]
10.10.10.2
10.10.10.3
```

### Changing the URL for a group

In the `hosts` file, you can change the URL for the page that will be displayed by changing the `dashboard_url` variable under the `[<GROUP_NAME>:vars]`

e.g.

```
[sport-dax:vars]
dashboard_url=http://www.bbc.co.uk/
```

# Troubleshooting

You might get this

```
$ ansible-playbook -i hosts <group_name>.yml

fatal: [10.10.36.91] => to use the 'ssh' connection type with passwords, you must install the sshpass program

$ brew install sshpass

Error: No available formula with the name "sshpass"
We won't add sshpass because it makes it too easy for novice SSH users to
ruin SSH's security.
```

In which case, you can do this

```
brew install https://raw.githubusercontent.com/kadwanev/bigboybrew/master/Library/Formula/sshpass.rb
```

> See https://gist.github.com/arunoda/7790979
