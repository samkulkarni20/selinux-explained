## What is SELinux
SELinux = Security Enhanced Linux

- It's a module in Linux Kernel
- Enabled by default in Fedora based OSes
- It controls access to files and/or processes
- 

## Modes
- Enforcing: Denies access if no allowing policy rule is found
- Permissive: Policy rules are not enforced. Denials based on policy rules are only logged.
- Disabled: Policy rules are neither enforced, nor logged. Only DAC rules control accesses.

## Manage SELinux modes
See the current mode
```
> getenforce
```

### Temp change
```
> # Set Permissive
> setenforce 0
> getenforce
Permissive
> # Set Enforcing
> setenforce 1
> getenforce
Enforcing
```

### Persistent Change
Update the SELINUX value in the file below to one of the 3 values mentioned in the file. 
**Reboot is required, if you only change this file & did not use `setenforce`**
```
> cat /etc/selinux/config

# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=enforcing
# SELINUXTYPE= can take one of these three values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```

## SELinux context
In below output `unconfined_u:object_r:user_tmp_t:s0` is called **SELinux Context** 

```
[root@rhel tmp]# ls -Z /tmp/cal.txt
unconfined_u:object_r:user_tmp_t:s0 /tmp/cal.txt
```
It has 4 parts:
- SELinux User
- Role
- Type
- Level

Following items in Linux system have SELinux Context attached to them & how to check the corresponding context info
- Files: `ls -Z`
- Processes: `ps -eZ`
- Users: `id` or `id -Z`