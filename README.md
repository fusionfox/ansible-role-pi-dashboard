# Before you start

- Download [NOOBS](https://www.raspberrypi.org/downloads/noobs/)
- Follow the [NOOBS setup guide](https://www.raspberrypi.org/help/noobs-setup/)
- When you boot the Pi for the first time, choose to download Raspbian
- Find out the IP address of your fresh Pi, and then use this tool

# Usage

Provision all hosts:

```bash
ansible-playbook -i hosts site.yml
```

> Warning, this really will provision **ALL** the Pi's listed in the `hosts` file, you probably want to be more specific

Provision a group of hosts (i.e. `tap-build-monitor`):

```bash
ansible-playbook -i hosts site.yml --limit tap-build-monitor
```

This will provision all Pi's that are in the `tap-build-monitor` group to dispay the URL specified in `group_vars/tap-build-monitor.yml`.

# Configuration

## Creating a new group

You will need to add a new group whenever you want to make a Pi point to a URL not already being used for a dashboard. 

If you just want to add a Pi to an existing group then see `Adding a pi to a group`.

### 1. New host group

In the `hosts` file, add a new block for your group that looks something like this

```
[<GROUP_NAME>]
<PI_IP_ADDRESS>
```

e.g.

```
[sport-dax]
10.10.10.2
```

### 2. New group variable

In the `group_vars` directory, create a new `<GROUP_NAME>.yml` file that looks something like this

```yaml
---
dashboard_url: <URL_TO_DISPLAY>
```

e.g.

```yaml
---
dashboard_url: http://10.10.36.91:3000/dashboard/db/sport-on-tap
```

## Adding a pi to a group

In the `hosts` file, you can add additional IP addressed under the `[<GROUP_NAME>]`

e.g.

```
[sport-dax]
10.10.10.2
10.10.10.3
```

## Changing the URL for a group

This is the webpage the pi will automatically display every time it starts up.

In the `group_vars` directory, edit the `<GROUP_NAME>.yml` file for the group you want to change

e.g.

```yaml
---
dashboard_url: http://www.bbc.co.uk/
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

```bash
brew install https://raw.githubusercontent.com/kadwanev/bigboybrew/master/Library/Formula/sshpass.rb
```

> See https://gist.github.com/arunoda/7790979
