# Run me

`ansible-playbook -i hosts pimon.yml`

# Suggested setup

- Download [NOOBS](https://www.raspberrypi.org/downloads/noobs/)
- Follow the [NOOBS setup guide](https://www.raspberrypi.org/help/noobs-setup/)
- When you boot the Pi for the first time, choose to download Raspbian
- Find out the IP address of your fresh Pi, and then use this tool

# Problems

You might get this

```
$ ansible-playbook -i openstack playbook.yml

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
