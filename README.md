# About

This script will install Perforce Server 2015.1 on a 64-bit linux host. I have use this successfuly to quickly setup a p4 server on Digital Ocean.

# Usage
Digital ocean:
1. Create Droplet, Ubuntu etc.
2. Add volume storage as required - this will be where our p4 data resides.  Follow the digital ocean guide to ssh in and mount new storage - remember the name of this mount.
3. IMPORTANT: Update both scripts in this repo so path matches the name of the new mount.

4. Run the following commands. You don't need to download this repo, that is what the first line in the following code does.

```shell
sudo wget https://raw.githubusercontent.com/bennymuller/linux-perforce-installer/master/install-perforce
sudo chmod +x install-perforce
sudo ./install-perforce
```

You will be asked to create a password and user details for a new unprivileged system user named `perforce`. You generally will never need to ever log into your server with this user, but I still suggest a password you won't lose. This is *not* a Perforce user, this is a Linux/Ubuntu user for the server only. You will create your Perforce user when you connect for the first time.

Afterwards, the server will restart and you should then be able to connect to your Perforce server.

# Security

Update .profile and .p4enviro to have new ip address of digital ocean server.
The created server will have default Perforce installation settings. This means anyone who connects to your server can create a user account without authorization. After you create your first user, you should close this security hole by using the following `p4` command from your Perforce Client.

        p4 configure set dm.user.noautocreate=2
