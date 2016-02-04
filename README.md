# Run me

`ansible-playbook -i hosts pimon.yml`

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
