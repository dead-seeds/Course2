In Unix, the environment variables are normally initialized 
during system startup by the system init startup scripts, 
and hence inherited by all other processes in the system

### Bash's quick assignment and inheritance trick
```LANGUAGE=he FOO=bar gedit```

When using this command, the new values are only assigned 
to the environment variables of the child process (in this
case gedit). The variables of the shell retain their original
values. The value of "LANGUAGE" will not change from its
original value, as far as subsequent commands to the shell are concerned.

### Session-wide environment variables
Suitable files for environment variable settings that should 
affect just a particular user (rather than the system as a whole)
are ```~/.profile```. After having edited one 
of those files, you should re-login in order to initialize the variables.

### System-wide environment variables

A suitable file for environment variable settings that 
affect the system as a whole (rather than just a particular
user) is ```/etc/environment```
example of the environmental file:
```
FOO=bar
EXAMPLE=value
```

### Environmental variables in FreeBSD

During the system init the system calls rc script
which calls other rc scripts. The boot script configuration files 
```
/etc/default/rc.conf
/etc/rc.conf
```
```/etc/rc.conf.local``` control the functioning of the rc script. 
The first of these files is installed by the operating system and 
should not be modified. The other two files contain overrides to 
settings in the first file.

#### Example of /etc/rc.conf file
```bash
accounting_enable="YES"
check_quotas="YES"
defaultrouter="192.168.29.204"
hostname="ada.ahania.com"
ifconfig_xl0="inet 192.168.29.216 netmask 255.255.255.0"
inetd_enable="YES"
nfs_client_enable="YES"
nfs_server_enable="YES"
portmap_enable="YES"
sendmail_enable="NO"
sshd_enable="YES"
```

## Access
There are 3 ways to read current environmental variables:
1. Third main parameter: `int main(int argc, char *argv[], char* envp[])`. Yes, there is a third one. It is standard (Irtegov verified)
2. Extern variable: `char **environ`
3. Systems calls: #syscall `putenv`, `setenv`
Third one is preferable to others because there is less space for error.

## Shell export
Other name for environmental variables is shell's exported variables. Shell has variables, and only exported ones will be in environment.

## Examples
1. PATH - list of directories to search binaries in. [[Unix]], contrary to [[Windows]], does not include current working directory by default. 
2. TZ - current timezone. If empty - look in /etc/TIMEZONE