zfs-mount-home
==============

### Mounting encrypted ZFS userhomes on login

Simple script and configuration for Debian's pam-auth-config to mount
encrypted ZFS file systems during user authentication.

Password for the encryption key is the user's password.

Note that the file system is not unmounted when last user process has
terminated. Once the file system has been mounted, data is accessible
to anyone with sufficient permissions.

### Installation

On a Debian system, do the following:

    # Specify your home dataset location in ZPATH_HOME
    % $EDITOR bin/zfs-mount-home

    # install files
    % sudo cp bin/zfs-mount-home /usr/local/sbin
    % sudo cp share/zfs-mount-home /usr/share/pam-configs

    # configure pam to enable zfs-mount-home
    % sudo pam-auth-config
