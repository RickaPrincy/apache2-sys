# **Apache2 Configuration with YAML Script**

---

This YAML script is designed to manage the configuration of an Apache2 server on a given host. It handles the configuration of all aspects related to the provided domain names.

Before using this script, make sure you have the root password for the host on which you want to configure Apache2, and the server has `openssh-server` installed.

You can also do it with ssh keys if you want,for that, you should read this [file](./ssh_key.md) first. 

## Get started 

### Server configuration

- Look for the line containing the directive `PermitRootLogin` on the file `/etc/ssh/sshd_config`. If it is commented out (starts with a #), remove the # symbol at the beginning of the line and set it to yes : `PermitRootLogin yes`.

If the PermitRootLogin line is already present and set to no, change it to yes.

- Then, restart ssh server with `sudo sytemctl restart ssh` the you should be able to log in as the root user using SSH.

### Launching the script

- Set your server's ip on the file `hosts` like this :

```sh
192.168.0.127
``` 
- Put all your domain names in the `domains` file:

```sh
www.example.com
abd.google.com
xyz.node.xyz
``` 

- Then run `script.yaml` with the following command :

```sh
ansible-playbook -i hosts script.yaml -k
```

- It will prompt for the `SSH pass`, which is the root password on the host (server).

- That's it! You just need to wait, and all of your sites with the domain names will be automatically configured.