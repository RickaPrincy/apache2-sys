# **Apache2 Configuration with YAML Script**

---

This YAML script is designed to manage the configuration of an Apache2 server on a given host. It handles the configuration of all aspects related to the provided domain names.

Before using this script, make sure you have the root password for the host on which you want to configure Apache2, and ensure that you have SSH access with a private SSH key for a user on the server (if the host is not your local machine, which means "localhost").

If you don't know how to do that, you can read [this file](./ssh_key.md).

# **Explanation of the Script's Functionality**

The YAML script is responsible for performing several tasks related to the configuration of an Apache2 server. Here's a breakdown of what the script does:

1. Creation of a `.conf` file in `/etc/apache2/sites-available`:
   - The script generates a configuration file in the `/etc/apache2/sites-available` directory. This file contains the necessary settings for each provided domain name and `activate that configuration.`
   - The configuration file ensures that Apache2 handles requests for the specified domain names correctly.

2. Creation of an appropriate directory in `/var/`:
   - The script creates a directory in the `/var/` path, specifically for each provided domain name.
   - These directories serve as the document roots for the respective websites associated with the domain names.

3. Creation of an `index.html` file for each domain name:
   - For each domain name provided, the script generates an `index.html` file within the corresponding directory in `/var/`.
   - The content of each `index.html` file is set to display a welcoming message specifically tailored to the corresponding domain name. For example, the content of `index.html` for the domain `www.example.com` would say "Welcome to www.example.com".

By executing this script, you automate the process of creating the necessary Apache2 configuration files, setting up the appropriate directories for the websites, and generating welcome pages for each domain name.

## How this script work ?

- First, you need to install Ansible on your local machine (where you want to run the script, not on the server).

- Change the `hosts` value in `script.yaml` to the IP address of the server or machine that you want to configure Apache2 on.

- Then, you should be able to run the script with the following command:
    
    ---

  - If you want to run the script on a remote host (not localhost):
    ```sh
    ansible-playbook --private-key=your_private_ssh_key --ask-become-pass --user=your_user script.yaml
    ```
    ---

  - If you want to run the script on a remote host and you use a passphrase for the SSH keys:
    ```sh
    ansible-playbook --private-key=your_private_ssh_key --ask-become-pass --ask-pass --user=your_user script.yaml
    # The --ask-pass option is added
    ```
    ---

  - If you are running the script on your local machine, simply use the command:
    ```sh
    ansible-playbook script.yaml --ask-become-pass
    ```

**Note**:

- Replace `your_private_ssh_key` with your private key and `your_user` with your username, which has access to the server using the private key.

- The command you choose will prompt for the `BECOME pass`, which is the root password on the host.

- Then, it will ask you where your `file is that contains all the domain names`. The file must contain something like:

```sh
www.example.com
abc.google.com
xyz.example.fr
```
## Automating the Execution of the Apache2 Configuration Script
I have developed a separate script to streamline the process of running this script automatically.
You can check the script [here](./automate.sh).