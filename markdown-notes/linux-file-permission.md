# File permissions in Linux

## Reading and modifying permissions

- Read: View a file or list directory contents
- Write: Create and modify a file or copy, move, and create files in a directory
- Execute: Execute or run a file or cd into a directory

Note a file name does not determine whether it is executable. It depends on the file's permissions.

Numerical values for read, write amd execute are explained below:

- Read (r) = 4
- Write (w) = 2
- Execute (x) = 1
- No permission (-) = 0

Permission value can range from 0 to 7 by adding the values above.

- Execute = 1
- Write = 2
- Write + Execute = 3
- Read = 4
- Read + Execute = 5
- Read + Write = 6
- Read + Write + Execute = 7

## Group permissions

There are four permission groups:

- User (u): The file owner
- Group (g): Other users in the file's group
- Others (o): All other users
- All (a): User, group, and others

Each linux file and directory is assigned read, write, and execute permissions for each of these groups.

## Changing the file permissions

You can change the file permissions by using `chmod` command.
