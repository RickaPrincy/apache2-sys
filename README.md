# **Apache2 Configuration with YAML Script**

---

This YAML script is designed to manage the configuration of an Apache2 server on a given host. It handles the configuration of all aspects related to the provided domain names.

Before using this script, ensure that you have `ansible` installed on your machine and also have the `root password` for the host where you want to configure Apache2. Additionally, make sure that the server has `openssh-server` installed.

You can also do it with `ssh keys` if you want,for that, you should read this [file](./ssh_key.md) first. 

## Server configuration

- Look for the line containing the directive `PermitRootLogin` on the file `/etc/ssh/sshd_config`. If it is commented out (starts with a #), remove the # symbol at the beginning of the line and set it to yes : `PermitRootLogin yes`.

If the PermitRootLogin line is already present and set to no, change it to yes.

- Then, restart ssh server with `sudo sytemctl restart ssh` then you should be able to log in as the root user using SSH.

## Get started 

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

### Launching the script with ssh keys

- You can launch the script with the following command if you use an SSH key to connect as root on the server and not with a root password

```sh
ansible-playbook -i hosts --private-key=your_private_ssh_key script.yaml
```
- If you have set a passphrase for the SSH keys:

```sh
ansible-playbook -i hosts --private-key=your_private_ssh_key --ask-pass script.yaml
# The --ask-pass option is added
```

- Replace `your_private_ssh_key` with your private key.

### Configure the local machine if you prefer using a root password instead of SSH keys

- You need to install `sshpass` on your local machine (the machine from which you will run the script.yaml playbook) to enable `password-based SSH authentication`.

    - Archlinux :

        ```sh
        sudo pacman -S sshpass
        ```
    - Debian :

        ```sh
        sudo apt install sshpass
        ```
- Make sure that the host's fingerprint is already configured. You can do this manually with the following command:

```sh
ssh <host>

#replace <host> with the IP address of the server
```

### Launching the script with root password

- You can run `script.yaml` with the following command :

```sh
ansible-playbook -i hosts script.yaml -k
```

- It will prompt for the `SSH pass`, which is the root password on the host (server).

### Accessing all domain names

Now you just need to configure a DNS server or add the following lines to the `/etc/hosts` file on each machine from which you want to access the domain names:

```sh
#server         domain
192.168.43.30   www.example.com
192.168.43.30   abd.google.com
192.168.43.30   xyz.node.xyz
```

## This should happen when you launch the script

- If you have completed all the configurations as mentioned and you run `script.yaml`, you should have something like :

![Result](/img/result.png "result")

- After configuring a DNS server or the `/etc/hosts` file, you should be able to access your sites like this:

![sys1Websites](/img/sys1.png "sys1")

