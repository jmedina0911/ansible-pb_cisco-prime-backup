CISCO PRIME BACKUP
==================
This playbook was created to generate and extract a Cisco Prime Backup from a NFS server.


Pre-requisites to run the playbook
----------------------------------
`expect` installed in NFS server, to ensure it is installed you could run the following command `/usr/bin/expect`

This playbook have been developed and tested under Ansble 2.10.2 and python version 3.6.9 on Ubuntu 18.4
You will require python, pip, git and ansible, and always is recommended to use a venv.

To install the requirements:
```
$ sudo apt-get update && sudo apt-get upgrade
$ sudo apt-get install -y build-essential libssl-dev libffi-dev python-dev
$ sudo apt-get install -y python3-pip
$ sudo apt-get install -y python3-venv

$ python3 -m venv venv
$ source ./venv/bin/activate
(venv) $ pip install --upgrade pip setuptools
(venv) $ pip install ansible
```


Variables
---------
**nfs_server** (str):
hostname of the NFS server where to store the backup files.
*Example*: ``10.200.5.1``

**nfs_user** (str):
username to login in the nfs server.

**nfs_password** (str):
password to login in the nfs server.

**prime_user** (str):
username to login in prime.

**prime_password** (str):
password to login in prime.


Run the playbook
----------------

#### Step
Clone and navigate to the repository dir:
```
git clone https://github.com/jmedina0911/ansible-pb_cisco-prime-backup
cd ansible-pb_cisco-prime-backup
```

#### Step
Create or use an inventory with the devices where to run the playbook

#### Step
Modify `ansible.cfg` to include the inventory created, for example:
```
[defaults]
host_key_checking = False
inventory = inventory.ini
```

#### Step
Before running playbook, test that inventory is available and configured properly.
```
ansible-inventory --list
```
#### Step
Run playbook adding the variables needed `nfs_user`, `nfs_password`, `prime_user`, `prime_password`

```
ansible-playbook pb_prime-backup.yml -e nfs_user=<nfs-user>  -e nfs_password=<nfs-pwd> -e prime_user=<prime-user> prime_password=<prime-pwd>
```

Notes:
------
The playbook is creating the backup in a Prime repository called `defaultRepo`, this repository should be created in Prime prior the excution, if your repository has different name just rename this in the code.

Future Improvements:
--------------------
Create a task to remove old backup files in Prime.

Example of execution:
--------------------
```
(venv):~/ansible-pb_cisco-prime-backup$ ansible-playbook pb_prime-backup.yml -e nfs_user=nfs_user -e nfs_password=nfs_user -e prime_user=prime_user -e prime_password=prime_password -v
Using /ansible-pb_cisco-prime-backup/ansible.cfg as config file

PLAY [prime] ***************************************************************************************************

TASK [RUN EXPECT FROM NFS SERVER TO GENERATE A BACKUPFILE]******************************************************
changed: [prime -> nfs_server] => {"censored": "the output has been hidden due to the fact that 'no_log: true' was specified for this result", "changed": true}

TASK [RUN EXPECT FROM NFS SERVER TO BRING THE BACKUP PERFORMED PREVIOUSLY] *************************************
changed: [prime -> nfs_server] => {"censored": "the output has been hidden due to the fact that 'no_log: true' was specified for this result", "changed": true}
```
