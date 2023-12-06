# Linux Basics

## Why Linux?

Many devops tools are built for Linux environments and some only run within Linux systems. 

## Linux basics

This course will cover
- Linux CLI
- VI Editor
- Package Management
- Service Management

Popular Linux Versions
- CentOS
- Ubuntu
- RedHat Enterprise Linux
- Suse
- Debian

This course will use CentOS as it is the most popular and is an open-source variant of RedHat Linux meaning that as you learn CentOS, you will understand much of RHEL as well. 

### Shell Types

- Bourn Shell (Sh Shell) Older
- C Shell (csh or tcsh)
- Z Shell (zsh)
- Bourne again shell (bash)

Find your current running shell:
```sh
> echo $SHELL
/bin/bash
```

### Commands
- echo      = print to screen
- ls        = list directory
- cd        = change directory
- pwd       = print working directory
- mkdir     = make new directory

Combine commands 
ie. 
```sh
> cd new_directory; mkdir www; pwd
/home/my_dir1/new_directory
```

#### Directory Commands

- mkdir
    + mkdir can be used to make single directories or entire directory trees
```sh
# will create the folder 'asia' in the tmp folder
mkdir /tmp/asia 
# will create india in the asia folder
mkdir /tmp/asia/india
# will create bangalore in the india folder
mkdir /tmp/asia/india/bangalore

# can be used to create a full directory tree with the -p flag
# all the sub-folders that do not currently exist will be created at once
mkdir -p /tmp/asia/india/bangalore
```

- rm
    + to remove a directory and all its contents, used the -r flag
```sh
rm -r /tmp/my_dir1
```

- cp
    + use the cp -r command to copy one drectory and all its files to another
```sh
cp -r /tmp/mydir1 /tmp/mydir2
```
#### Files Commands

- touch
    + create a new, empty file
```sh
touch new_file.txt
```

- cat
    + Add contents to a file
    ```sh
    cat > new_file.txt 
    This is some new content
    # CTLR + D to complete contents to add
    ```
    + Output the contents of a file to the screen
    ```sh
    cat new_file.txt
    ```
- cp 
    + Copy file
    ```sh
    cp file.txt copyfile.txt
    ```
- mv
    + Move or rename file
    ```sh
    # to move a file
    mv ./file1.txt ./newdirectory/file1.txt
    # to rename a file
    mv ./file1.txt ./file2.txt
    ```
## KodeKloud Labs

Dedicated learning labs for students to get fast access to infrastructure to speed learning

## VI Editor

### Command Mode
Command mode cannot insert new text but can be used to delete as well as copy and paste.
- Arrow keys to move around
- Delete = X for character dd for line
- Copy and Paste = yy copy, p paste
- Scroll = up CTRL+u down CTRL+d
- Command = :
- Save = :w to add a filename ':w filename'
- Quit (discard changes) = :q 
- Save and Quit = :wq
- Find = / to go to next instance press 'n' 
    + example: to fine the word 'next' use '/next' if the instance isn't the correct one, press 'n' to go to the next instance of the word.

## More linux commands
- whoami = shows the current logged on user
- id = shows information about the current logged on user
- su = changes the current user (switch user)
    + example 'su johnb' will change to the user johnb and ask for the password for that account to continue.
- ssh = login to another linux box format is username@hostname (can also use hostIP)
    + example
    ```sh
    ssh johnb@192.168.0.2
    ```
### User accounts
Every system has a root user that can perform all tasks on the system. Access to the root should be restricted and you should never logon usiogn the root user account. 

If a task can normally only be done by a root account, a normal user can be granted temporary root permissions using the 'sudo' command.

When sudo is invoked, the user must enter their password again. 

### Downloading files
- curl = used to print files to screen or can be used to download a file using the -o flag
    + example
    ```sh
    curl https://www.somesite.com/somefile.txt -o
    ```
- wget = also used to download files 
    + example
    ```sh
    wget https://www.somesite.com/somefile.txt -o somefile.txt
    ```
### Check OS Version
To check the OS version you can inspect the release files
- ls /etc/*release*
- cat /etc/*release*

## Package Management
Packages are bundled into RPM (Redhat package manager) files
- rpm = used to manage RPM packages
    + rpm -i = install a package
    ```sh
    rpm -i telenet.rpm
    ```
    + rpm -e = uninstall a package
    + rpm -q = query a package

RPM requires you to point at a specific package to install and doesn't care about dependencies that package may have. For example, if a software package required gcc to compile a version of itself, it will not install gcc and assumes that you will have done that already. 

### YUM
- YUM = a high level package manager that uses RPM and manages software dependencies.
    + Yum searches cloud and local repositories, if configured, to find RPM files to install allong with dependancies in the required order. 
    + Yum repos are referenced in /etc/yum.repos.d
    + Every Linux opererating system comes with its own set of bundled repositories. 
    + You can add repositories as needed

To see a list of configured repos, run the 'yum repolist' command
To see the repo filenames, use:
```sh
ls /etc/yum.repos.d
```

To review the settings for a repo, you can use cat
```sh
cat /etc/yum.repos.d/CentOS-Base.repo
[extras]
name=CentOS-$releasever - Extras
baseurl=https://mirror.centos.org/centos/$releasever/extras/$baseearch/
...
```
#### Yum Commands
- yum list = Lists available packages
    + example
    ```sh
    yum list ansible
    Installed Packages
    ansible.noarch      2.9.6-1.el7             @EPEL
    ```
- yum remove = removes an installed package
    + example
    ```sh
    yum remove ansible
    ```
- yum --showduplicates list = shows all versions of a package that are available
    + example
    ```sh
    yum --showduplicates list ansible
    Available Packages
    ansible.noarch      2.4.2.0-2.el7           extras
    ansible.noarch      2.9.6-1.el7             epel
    ```
- yum install = to install a specific version of a package
    + example
    ```sh
    yum install ansible-2.4.2.0
    ```

### Services
Ensure that processes run in the background and startup in order at server start.

Starting a service:
two methods:
- service servicename start (older version, currently an alias for systemctl)
- systemctl start servicename (newer method, use this one)

Stop a service
- systemctl stop servicename

Check the state of a service
- systemctl status servicename

Set a service to start at boot
- systemctl enable servicename

Disable a service from starting at startup
- systemctl disable servicename

#### Configure an application as a service

You have an app /usr/bin/python3 /opt/code/my_app.py
When you run the applation, it runs a simple web site with a simple message:
```sh
curl http://localhost:5000

Hello, World!
```

You want to have the application start at bootup and be available whenever you run the curl command to get the output. 

Services are kept in the path '/etc/systemd/system'

Create a file with the name you want the service to be called and add the options for the service to run with:

```sh
touch my_app.servce
vi my_app.service

[Service]
ExecStart=/usr/bin/python3 /opt/code/my_app.py

```

Run 'systemctl daemon-reload' to relead the service configuration files from '/etc/systemd/system'

run 'systemctl start my_app' to start the new service created from your app.

run 'systemctl status my_app' to verify the status of the service

To set the service at bootup, set the service to run after another service that runs at bootup by adding an Install section to the service file.

```sh
[Service]
ExecStart=/usr/bin/python3 /opt/code/my_app.py

[Install]
WantedBy=multi-user.target
```
Then run 'systemctl enable my_app' to set the service to run at startup

In the serivce configuration file, there are other directives that can be configured.

```sh
[Unit]
Description=My Python Web Application 

[Service]
ExecStart=/usr/bin/python3 /opt/code/my_app.py
ExecStartPre=/opt/code/RunBeforeMy_App.sh
ExecStartPost=/opt/code/RunAfterMy_App.sh
Restart=always
# sets the service to always restart if it crashes

[Install]
WantedBy=multi-user.target
```













    




