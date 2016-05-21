# GR Ansible
Ansible scripts for server and application zero downtime deployment / redeployment


# Team Brioche
A super talented team of BCIT students, tasked with creating a rolling redeployment and deployment
solution via ansible for a client.

Members include:

*Celia Lee
*Patrick Voth
*Cooper Worobetz
*Liam Wyatt

# Overview

This script contains three playbooks and several roles.

## gce.yml

This playbook uses several roles to effectively generate a working environment for use in the rolling redeploy. This includes creating scalable load balancers, webservers and monitoring servers. There is more detail on the environment it creates later in this file.


## redeploy.yml

This playbook uses a single role, briochebcit.redeploy, to loop through a rolling redeploy. This is done in two stages, the first being on the first 60% of webservers, and the second being on the remaining servers. 


## loop.yml
This file performs a rolling redploy as a self-contained script. However, it is depreciated in favour of the other, role based, playbooks.


