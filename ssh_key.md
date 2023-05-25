# **Generating and Using SSH Keys**

This file provides instructions on how to generate and use `SSH keys` using `ssh-keygen` and `ssh-copy-id` to send a `public key`; as well as how to connect to a server using the `private key.

## 1. Generating the SSH Keys

- Run the following command to generate a new SSH key pair: 
```sh
    ssh-keygen -t rsa -b 4096 -f private.key
```
This command generates an RSA key pair with a key length of 4096 bits and saves the private key as private.key.

- You will be prompted to provide a `passphrase`. You can choose to enter a passphrase or leave it empty for no passphrase. Note that setting a passphrase adds an extra layer of security.

- The command will generate two files: private.key (the private key) and private.key.pub (the public key).

## 2. Copying Public Key to Remote Server

- Run the following command to copy the public key to the remote server:
```sh
ssh-copy-id -i private.key.pub username@ip

#for the script.yaml, the username must be "root"
```
- Replace private.key.pub with the actual path to your public key file, username with the username on the remote server, and ip with the server's IP address.

- You will be prompted to enter the password for the remote server. Enter the password to authenticate and copy the public key.

**Note**: If you have set a passphrase for your private key, you will be prompted to enter it before copying the key.

- The public key will be added to the `~/.ssh/authorized_keys` file on the remote server, allowing you to authenticate using the private key.

- `ssh-copy-id -i private.key.pub root@ip` will not work if you don't set the `PermitRootLogin` to `yes` ( it's mentionned on [README.md](./README.md) )

## 3. Connecting to Server using Private Key
- Run the following command to connect to the server using the `private key`:

```sh
ssh -i private.key username@ip
```
Replace private.key with the actual path to your private key file, username with the username on the remote server, and ip with the server's IP address and that's it, you are connected to the server.

**Note** : 
- If you set a passphrase for your private key, you will be prompted to enter it.

- Remember to keep your private key secure and never share it with unauthorized individuals. Additionally, it's good practice to set strong passphrases for your private keys to enhance their security.