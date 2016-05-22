# GR Ansible
Ansible scripts for server and application zero downtime deployment / redeployment


# Team Brioche
A super talented team of BCIT students, tasked with creating a rolling redeployment and deployment
solution via ansible for a client.

Members include:

Celia Lee
Patrick Voth
Cooper Worobetz
Liam Wyatt

# Overview

This script contains three playbooks and several roles.

## gce.yml

This playbook uses several roles to effectively generate a working environment for use in the rolling redeploy. This includes creating scalable load balancers, webservers and monitoring servers. There is more detail on the environment it creates later in this file.


## redeploy.yml

This playbook uses a single role, briochebcit.redeploy, to loop through a rolling redeploy. This is done in two stages, the first being on the first 60% of webservers, and the second being on the remaining servers.


## loop.yml
This file performs a rolling redploy as a self-contained script. However, it is depreciated in favour of the other, role based, playbooks.



# The Environment

The playbook gce.yml creates and configures an environment on the Google Cloud platform consisting of:

## lb-server-# (scalable)

A load balancing server that utilised HAProxy, a popular and free proxy/load balancing solution. This server also has a munin-node installed on it to monitor it.

## munin-server-# (scalable)

A monitoring server via munin, popular client-slave based monitoring software. Requires all monitored nodes to have munin-node installed and configured, which is part of the gce.yml.

## web-server-# (scalable)

A simple webserver, using apache 2.4 and php 5. A basic webapp is installed by default from one of our public repositories.


## All scalable servers can have specified numbers made via modifying the hosts file

# The Rolling Redeployment

The playbook redeploy.yml performs a simple rolling redeploy. In the first stage, ~%60 of the servers are taken out of the HAproxy pool, updated via templating an index.php with a timestamp into it's www directory, and then added back into the pool.
