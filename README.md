# **Apache2 Configuration with `YAML` Script**

<hr>

This YAML script is designed to manage the configuration of an Apache2 server on a given host.
It handles the configuration of all aspects related to the provided domain names.

Before using this script, make sure you have the `root password` for the host on which you want to configure `Apache2`, and ensure that you have SSH access with a `private SSH` key for a user on the server (if the host is not your local machine, wich means `localhost`).

##If don't know how to do that, you can read [this file](./ssh_key.md).

## Usage Instructions
- First, you need to install ansible on your local machine (where you want to run the script, not on the server).

- Then, you should be able to run the script with the following command:
- - To execute the script on a remote host (not localhost) :

```sh
ansible-playbook --private-key=your_private_ssh_key --ask-become-pass --user=your_user script.yaml
```

- - If you are running the script on your local machine, simply use the command :

```sh
ansible-playbook script.yaml --ask-become-pass
```
**Note**: 
- It will prompt a `BECOME pass`, it's the `root password on the host` 
- Replace `your_private_ssh_key` with your private key and `your_user` with your username, which has access to the server using the private key.