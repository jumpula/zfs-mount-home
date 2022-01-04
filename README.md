zfs-mount-home
==============

### Mounting encrypted ZFS userhomes on login

Simple script and configuration for Debian's pam-auth-config to mount
encrypted ZFS file systems during user authentication.

Password for the encryption key is the user's password.

Note that the file system is not unmounted when last user process has
terminated. Once the file system has been mounted, data is accessible
to anyone with sufficient permissions.

Also note that if user's password is forgotten, user's home cannot be
decrypted.

### Installation

On a Debian system, do the following:

    # Specify your home dataset location in ZPATH_HOME
    % $EDITOR bin/zfs-mount-home

    # install files
    % sudo cp bin/zfs-mount-home /usr/local/sbin
    % sudo cp share/zfs-mount-home /usr/share/pam-configs

    # if you use schroot
    % sudo cp setup.d/12mountuserhome /etc/schroot/setup.d

    # configure pam to enable zfs-mount-home
    % sudo pam-auth-config

### Creating a dataset for user's home

Create a dataset for user as follows:

    # Use the same password as you do for user authentication
    % zfs create \
        -o encryption=aes-256-gcm \
        -o keyformat=passphrase \
        -o keylocation=prompt \
        -o canmount=noauto \
        pool/path/to/home/$USER
