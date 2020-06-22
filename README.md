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
- Install wordpress related icigna2 checks
- Install appropriate apache2 configuration and enable php module for apache
