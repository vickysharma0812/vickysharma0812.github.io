# Managing Groups in Linux

## Creating a group 

We can create a group using the `groupadd` command as shown below:

```bash
sudo groupadd groupname
```

You can change the properties of a group using the `groupmod` command. For example, to change the group name, you can use the following command:

```bash
sudo groupmod -n newgroupname oldgroupname
```

## Deleting a group

You can delete a group using the `groupdel` command as shown below:

```bash
sudo groupdel groupname
```

## Adding a user to a group

You can add a user to a group using the `usermod` command as shown below:

```bash
sudo usermod -a -G groupname username
```

It is important to use the `-a` option (append) along with `-G` option to avoid removing the user from other groups.

## Removing a user from a group

You can remove a user from a group using the `gpasswd` command as shown below:

```bash
sudo gpasswd -d username groupname
```

