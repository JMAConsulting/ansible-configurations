# Introduction

This repository contains all the ansible configuration needed to install a new server for JMA Consulting needs

# Execution

1. Ensure that you have ssh access to the server and that you can sudo as your user
2. Ensure that you have ansible installed locally or wherever you are running this from.
3. Update the production file with the information about which groups the new server should be associated and which roles it will execute
4. Run `ansible-playbook -K -i production  -l <fdqn of the new server> ./site.yml`

If you only want to run part of the playbook e.g. the part associated with PHP then run `ansible-playbook -K -i production  -l <fdqn of the new server> --tags php ./site.yml` 

# To DO
- Cover installing clamav and setting up a daily scanning job
- create users + sudo access for JMA staff on servers as appropriate
- Set up icigna2 master node sensibly
- set up sshd configuration sensibly.
- Execute to set standard configuration for opha as well.

# Details of configuration structure

Hosts and groups that the host is part of is in the production file / inventory. Eeach host belongs to one or more groups and at the very least it belongs in the [server:children] group. The roles each group inherits is then contained in the `site.yml` file which specifies for each group what roles they should execute. The roles are then defined as sub folders within the roles folder. At the very least a role will have a tasks folder with a `main.yml` file.

Variables can be used within roles e.g. `{{ php_version }}`. A role can and should provide a default for that which is generally found in the `<role name>/defaults/main.yml` file. However it may be necessary to set global defaults which are stored in the `group_vars/all` file or if a specific host needs to override the default e.g. in RH2 we need to use PHP7.1 because of the age of the CMS and CRMs on that host we then set it in the `host_vars/<fdqn of the server>` file e.g. `host_vars/rh2.jmaconsulting.biz`

Within each role they can use functions to create files / templates based on stored templates within their role and depending on the host type you can determine if certain steps are to be run or not run.
