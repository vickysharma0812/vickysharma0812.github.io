# Managing users in Linux

## Creating a user account

We will look at two common commands used to create user accounts in linux:

- useradd
- adduser

The useradd command is simple for adding a new user to the system.

```bash
sudo useradd vikas
```

We can also specify the password for username using the `passwd` command.

```bash
sudo passwd vikas
```

On some linux distribution `adduser` command is a symbolic link to `useradd` command. However, in some distributions it is an interactive perl script that guides you through the process of adding a user.

The entries of a user lives in the `/etc/passwd` file. 

## Changing user information 

You can change user information using the `usermod` command. 

For example, we can add a user to a group using the following command:

```bash
sudo usermod -a -G groupname username
```


It is important to use the `-a` option (append) along with `-G` option to avoid removing the user from other groups.


- `-s` option is used to change the login shell of the user.
- `-e` option is used to set the account expiration date.
- `-d` option is used to change the home directory of the user.

## Removing a user account

You can remove a user account using the `userdel` command. The entry of the user will be removed from the `/etc/passwd` file. However, the home directory and files of the user will remain intact.

You can delete the home directory and files of the user using the `-r` option as shown below:

## Changing password expiration information

The chage command changes the number of days between password changes and the last password change date. The system uses this information to determine when users must change their passwords



