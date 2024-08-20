[Home](../README.md)

### Systemd

#### Systemd
Systemd is designed to provide a complete solution for system startup and management.

According to Linux conventions, the letter **d** is the abbreviation for daemon. 
So the meaning of the name Systemd is that it guards the entire system.

Now you don't need to use **init** anymore. Systemd takes the place of 
**initd**, and it becomes the first process of the system (PID is 1), and 
other processes are its child processes.
```
$ systemctl --version
```
The above command is used to check the version of Systemd.

The advantages of Systemd are that it's powerful and easy to use. The 
disadvantages are that it's huge and complex. In fact, ​many people opposes 
Systemd on the grounds that it is too complex and strongly coupled with the 
rest of the operating system, and they think that it violates the Unix 
philosophy of "keep simple, keep stupid".

![Systemd Architectire](../images/systemd_command_1.png)
(The Systemd architecture diagram)

#### System Management
Systemd doesn't mean a command, but means a set of commands that cover all 
aspects of system management.

##### systemctl
`systemctl` is the main command of Systemd for managing systems.
```
# Reboot the system
$ sudo systemctl reboot

# Turn off the system and cut off the power
$ sudo systemctl poweroff

# CPU stops working
$ sudo systemctl halt

# Suspend the system
$ sudo systemctl suspend

# System enters the hibernate state
$ sudo systemctl hibernate

# System enters the hybrid-sleep state
$ sudo systemctl hybrid-sleep

# Start to enter rescue state (single user status)
$ sudo systemctl rescue
```

##### systemd-analyze
The `systemd-analyze` command is used to view the time for the startup.
```
# View the startup time
$ systemd-analyze                                                                                       

# View the startup time of each service
$ systemd-analyze blame

# Show the startup process flow
$ systemd-analyze critical-chain

# Show the startup flow of the specified service
$ systemd-analyze critical-chain atd.service
```

##### hostnamectl
The `hostnamectl` command is used to view information about the current host.
```
# Show the information about the current host
$ hostnamectl

# Set the host name
$ sudo hostnamectl set-hostname rhel7
```

##### timedatectl
The `timedatectl` command is used to view the current time zone settings.
```
# View the current time zone settings
$ timedatectl

# Show all the available time zones
$ timedatectl list-timezones                                                                                   

# Set the current time zone
$ sudo timedatectl set-timezone America/New_York
$ sudo timedatectl set-time YYYY-MM-DD
$ sudo timedatectl set-time HH:MM:SS
```

#####  loginctl
The `loginctl` command is used to view the currently logged-in users.
```
# List the current sessions
$ loginctl list-sessions

# List the currently logged-in users
$ loginctl list-users

# List the information showing the specified user
$ loginctl show-user ruanyf
```

#### Unit

##### Unit
Systemd can manage all system resources. All of the different resources 
are collectively referred to as Unit.

We can divide the Unit into 12 types.
* Service unit: system service
* Target unit: A group of multiple units
* Device Unit: Hardware device
* Mount Unit: Mount point of the file system
* Automount Unit: Auto Mount Point
* Path Unit: file or path
* Scope Unit: An external process that is not started by Systemd
* Slice Unit: Process Group
* Snapshot Unit: Systemd snapshot; you can switch back to a certain snapshot
* Socket Unit: Socket for interprocess communication
* Swap Unit:swap file
* Timer Unit: Timer

The `systemctl list-units` command can be used to view all the Units of 
the current system.
```
# List the running Unit
$ systemctl list-units

# List all the Units, including the ones which doesn't find the configuration file or fails to start
$ systemctl list-units --all

# List all the Units that doesn't run
$ systemctl list-units --all --state=inactive

# List all the Units that fails to load
$ systemctl list-units --failed

# List all the running Units of which type is service
$ systemctl list-units --type=service
```

##### Status of Unit
The systemctl status command is used to view the system status and the status of a single unit.

```
# Display the system status
$ systemctl status

# Display the status of a single unit
$ sysystemctl status bluetooth.service

# Display the status of a unit on the remote host
$ systemctl -H root@rhel7.example.com status httpd.service
```
In addition to the status command, systemctl also provides three simple 
methods for querying the status, which are mainly used in the judgment 
statement in the script.
```
# Show whether a Unit is running
$ systemctl is-active application.service

# Show whether a Unit is in a boot failure state
$ systemctl is-failed application.service

# Show whether a Unit service has established an enabled link
$ systemctl is-enabled application.service

```

##### Unit Management
The most common commands are the following ones which are used for starting 
and stopping Unit (service mainly).
```
# Start a service
$ sudo systemctl start apache.service

# Stop a service
$ sudo systemctl stop apache.service

# Restart a service
$ sudo systemctl restart apache.service

# Kill all the child processes of a service
$ sudo systemctl kill apache.service

# Reload the configuration files of a service
$ sudo systemctl reload apache.service

# reload all the modified configuration files
$ sudo systemctl daemon-reload

# Show all the underlying parameters of a Unit
$ systemctl show httpd.service

# Show the value of the specified property of a Unit
$ systemctl show -p CPUShares httpd.service

# Set the specified property of a Unit
$ sudo systemctl set-property httpd.service CPUShares=500
```

##### Dependencies
If Unit A depends on Unit B, then Systemd will start Unit B when it starts Unit A.

The systemctl list-dependencies command is used to list all the dependencies of a Unit.
```
$ systemctl list-dependencies nginx.service
```
Some dependencies of the output for the above command are of the type Target, 
and it won't be expanded by default. If you want to expand Target, you 
need to use the --all parameter.
```
$ systemctl list-dependencies --all nginx.service
```

#### Unit Configuration Files
##### Configuration files
Each Unit has a configuration file that tells Systemd how to start the Unit.

By default, Systemd reads the configuration file from the directory 
`/etc/systemd/system/`. However, most of the files stored inside are symbolic
 links, which point to the directory `/usr/lib/systemd/system/`, and the real 
 configuration files are stored in this directory.

The `systemctl enable` command is used to establish a symbolic link 
relationship between the two directories above.
```
$ sudo systemctl enable clamd@scan.service
# which is equivalent to
$ sudo ln -s '/usr/lib/systemd/system/clamd@scan.service' '/etc/systemd/system/multi-user.target.wants/clamd@scan.service'
```
If you have set powerboot in the configuration file, the `systemctl enable` 
command is equivalent to activating it.

Correspondingly, the `systemctl disable` command is used to revoke the 
symbolic link relationship between the two directories, which is 
equivalent to canceling the boot.
```
$ sudo systemctl disable clamd@scan.service
```
The suffix name of the configuration file is the type of the Unit, such as 
`sshd.socket`. If omitted, Systemd will set the suffix name to `.service` 
by default, so `sshd` will be interpreted as `sshd.service`.

##### Status of the configuration file
The `systemctl list-unit-files` command is used to list all configuration files.
```
# List all the configuration files
$ systemctl list-unit-files

# List the configuration files of the specified type
$ systemctl list-unit-files --type=service
```
This command will output a list.
```
$ systemctl list-unit-files

UNIT FILE              STATE
chronyd.service        enabled
clamd@.service         static
clamd@scan.service     disabled
```
There are four status for each configuration file.

* enabled: It has been established the enabled link.
* disabled: It has not established the enabled link.
* static: The configuration file does not have the [Install] section 
    (cannot be executed), so it can only be used as a dependency of other 
    configuration files.
* masked: The configuration file is forbidden to establish an enabled link.
> Note that we can't know from the status of the configuration file whether 
> the Unit is running. Here we need to execute the systemctl status command 
> mentioned earlier.

```
$ systemctl status bluetooth.service
```
Systemd needs to reload the configuration file and restart it as long as the 
configuration file is modified, otherwise the modification will not take effect.
```
$ sudo systemctl daemon-reload
$ sudo systemctl restart httpd.service
```

##### Format of the configuration file
Configuration files are plain text files that can be opened with a text editor.

The `systemctl cat` command can be used to view the contents of the configuration file.
```
$ systemctl cat atd.service

[Unit]
Description=ATD daemon

[Service]
Type=forking
ExecStart=/usr/bin/atd

[Install]
WantedBy=multi-user.target
```
As you can see from the output above, the configuration file is divided into 
several blocks. The first line of each block is the distinguished name which 
is in square brackets, such as **[Unit]**. Note that the block name and field name 
of the configuration file are case sensitive.

Inside each block are some key-value pairs connected with equal sign.
```
[Section]
Directive1=value
Directive2=value

. . .
```
> Note that there must be no spaces on either side of the equal sign of the key-value pairs.

##### Blocks of configuration files
The **[Unit]** block is usually the first block of the configuration file, 
and it's used to define the metadata for the Unit and configure the relationship
to other Units. Its main fields are as follows.

* Description
* Documentation: Document Address
* Requires: Other Units that the current Unit depends on. If they are not 
            running, the current Unit will fail to start.
* Wants: Other Units that work with the current Unit. If they are not 
         running, the current Unit will not fail to start.
* BindsTo: Similar to Requires. If the Unit specified by it exits, it will 
           cause the current Unit to stop running.
* Before: If the Unit specified by this field is also to be started, it must 
          be started after the current Unit.
* After: If the Unit specified by this field is also to be started, it must be 
         started before the current Unit.
* Conflicts: The Unit specified here cannot be run simultaneously 
             with the current Unit.
* Condition...: The condition that the current Unit must satisfy, otherwise 
                it will not run.
* Assert...: The condition that the current Unit must satisfy, otherwise 
             it will fail to start.

**[Install]** is usually the last block of the configuration file, and it's 
used to define how to start, and whether it starts up automatically. Its main
fields are as follows.

* WantedBy: Its value is one or more Targets. When the current Unit is enabled, 
            the symbolic link will be placed in the subdirectory consisting of 
            the Target name + .wants suffix which is under the 
            `/etc/systemd/system` directory.
* RequiredBy: Its value is one or more Targets. When the current Unit is 
              enabled, the symbolic link will be placed in the subdirectory 
              consisting of the Target name + .required suffix. which is 
              the `/etc/systemd/system` directory.
* Alias: The alias ​​that the current Unit can be used to start
* Also: Other Units that will be enabled at the same time when the current 
        Unit is enabled.

The **[Service]** block is used for the configuration of the Service. Only 
the Unit of the type Service has this block. Its main fields are as follows.

* Type: Define the behavior of the process at startup. Its values are as follows.
* Type=simple: The default value. It executes the command specified by 
               ExecStart, and starts the main process.
* Type=forking: Create a child process from the parent process in the fork 
                mode. After the creation, the parent process will exit immediately.
* Type=oneshot: One-time process. Systemd will wait for the current service 
                to exit, and then move on executing.
* Type=dbus: The current service is started by D-Bus.
* Type=notify: After the current service finishes starting, it will notify 
               Systemd, and then go on executing.
* Type=idle: The current service will run only after other tasks have finished executing.
* ExecStart: The command to start the current service.
* ExecStartPre: The command executed before starting the current service.
* ExecStartPost: The command executed after starting the current service.
* ExecReload: The command executed when restarting the current service.
* ExecStop: The command executed when stopping the current service.
* ExecStopPost: The command executed after stopping the current service.
* RestartSec: The number of seconds of the interval for restarting the 
              current service automatically.
* Restart: Define the circumstances on which Systemd will restart the current 
           service automatically, and its possible values ​​include always, 
           on-success, on-failure, on-abnormal, on-abort, on-watchdog.
* TimeoutSec: Define the number of seconds Systemd waits before stopping the current service.
* Environment: Specify the environment variables.

Go to the [official documentation](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) 
for the complete list of the Unit configuration files.

##### Target
It needs to start a large number of Units when starting the computer. So, it 
is obviously inconvenient if we need to write out each time which Units are 
needed for the startup. The solution provided in Systemd is Target.

Simply put, Target is a Unit group with many related Units. When a Target is 
started, Systemd will start all the Units inside the Target.

In the traditional `init` startup mode, there is a concept of RunLevel, which 
is similar to the role of Target. The difference is that RunLevel is mutually 
exclusive, so it's not possible to start multiple RunLevels at the same time; 
But multiple Targets can be started at the same time.
```
# View all the Targets of the current system.
$ systemctl list-unit-files --type=target

# View all the Units included in a Target.
$ systemctl list-dependencies multi-user.target

# View the default target at startup.
$ systemctl get-default

# Set the default Target that is at the startup.
$ sudo systemctl set-default multi-user.target

# When switching Targets, the process started by the previous Target won't be closed by default.
# The systemctl isolate command can be used to change this behavior:
# Close all the processes which are in the previous Target but won't be used in the next Target.
$ sudo systemctl isolate multi-user.target
```
The correspondences between the Target and the traditional RunLevel are as follows.
```
Traditional runlevel      New target name     Symbolically linked to...

Runlevel 0           |    runlevel0.target -> poweroff.target
Runlevel 1           |    runlevel1.target -> rescue.target
Runlevel 2           |    runlevel2.target -> multi-user.target
Runlevel 3           |    runlevel3.target -> multi-user.target
Runlevel 4           |    runlevel4.target -> multi-user.target
Runlevel 5           |    runlevel5.target -> graphical.target
Runlevel 6           |    runlevel6.target -> reboot.target
```
The main differences between it and the `init` process are as follows.

1. The default RunLevel (can be set in the `/etc/inittab` file) is now 
replaced by the default Target. The default Target locates in 
`/etc/systemd/system/default.target`, which is usually symbolically linked to 
`graphical.target` (graphical interface) or `multi-user.target` 
(multi-user command line).

2. The previous startup script locates in the `/etc/init.d` directory, which 
is symbolically linked to different RunLevel directories (such as `/etc/rc3.d`,
`/etc/rc5.d`, etc.), while it is now stored in the `/lib/systemd/system` and 
`/etc/systemd/system` directories.

3. The previous location of the configuration file: The configuration file of 
the init process is `/etc/inittab`, and the configuration files of various 
services are stored in the `/etc/sysconfig` directory; The configuration file 
now is mainly stored in the `/lib/systemd` directory, and the the original 
settings can be overridden by modifying in the `/etc/systemd` directory.

##### Log Management
Systemd manages the startup logs for all Units. So you can view all the logs 
(kernel logs and application logs) with just one command of `journalctl`. The 
configuration file for the log is `/etc/systemd/journald.conf`.

The command `journalctl` is very powerful.
```
# View all the logs (Only the logs started this time are saved by default.)
$ sudo journalctl

# View the kernel logs (The application logs are not displayed.)
$ sudo journalctl -k

# View the logs that are started this time.
$ sudo journalctl -b
$ sudo journalctl -b -0

# View the logs that were last started (you need to change the settings).
$ sudo journalctl -b -1

# View the logs for the specified time.
$ sudo journalctl --since="2012-10-30 18:17:16"
$ sudo journalctl --since "20 min ago"
$ sudo journalctl --since yesterday
$ sudo journalctl --since "2015-01-10" --until "2015-01-11 03:00"
$ sudo journalctl --since 09:00 --until "1 hour ago"

# Show the logs of the last 10 lines.
$ sudo journalctl -n

# Show the logs of the last specified lines.
$ sudo journalctl -n 20

# Show the latest logs in real time.
$ sudo journalctl -f

# View the logs of the specified service
$ sudo journalctl /usr/lib/systemd/systemd

# View the logs of the specified process
$ sudo journalctl _PID=1

# View the logs of a script for a path
$ sudo journalctl /usr/bin/bash

# View the logs of the specified user
$ sudo journalctl _UID=33 --since today

# View the logs of a Unit
$ sudo journalctl -u nginx.service
$ sudo journalctl -u nginx.service --since today

# Show the latest logs of a Unit in real time.
$ sudo journalctl -u nginx.service -f

# Merge and show the logs of multiple Units.
$ journalctl -u nginx.service -u php-fpm.service --since today

# View the logs of the specified priority level (and above), and there are 8 levels.
# 0: emerg
# 1: alert
# 2: crit
# 3: err
# 4: warning
# 5: notice
# 6: info
# 7: debug
$ sudo journalctl -p err -b

# The output for logs is paging by default. You can use --no-pager to change it to normal standard output.
$ sudo journalctl --no-pager

# Output in the JSON format (a single line).
$ sudo journalctl -b -u nginx.service -o json

# Output in the JSON format (multiple lines), which is more readable.
$ sudo journalctl -b -u nginx.serviceqq
 -o json-pretty

# Show the hard disk space occupied by the logs.
$ sudo journalctl --disk-usage

# Specify the maximum space that can be occupied by the log file
$ sudo journalctl --vacuum-size=1G

# Specify how long the log file will be saved.
$ sudo journalctl --vacuum-time=1years
```

Resources:
* [TutorialDocs](https://www.tutorialdocs.com/article/learn-systemd-commands-in-20-minutes.html) (*this is the best I think*)
* [SoftPrayog](https://www.softprayog.in/tutorials/systemd-system-and-service-manager-in-linux)
* [Hostinger](https://www.hostinger.com/tutorials/manage-and-list-services-in-linux/)
* [linux.com](https://www.linux.com/training-tutorials/managing-services-linux-systemd/)
* [Linux Journal](https://www.linuxjournal.com/content/initializing-and-managing-services-linux-past-present-and-future)