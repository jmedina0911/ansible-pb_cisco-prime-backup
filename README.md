CISCO PRIME BACKUP
==================
This playbook was created to generate and extract a Cisco Prime Backup from a NFS server.


System Requirements
-------------------
`expect` installed in NFS server.


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
