# Ansible assignment

## Create instance in google cloud

First the playbook will create the two web-server and the db-server instances in google cloud using gcp module with service account.

The template to do that is `manage_instance.yml`

We will use a dynamic inventory with the `gcp_compute` module. Hosts group will be created dynamically and temporary for the playbook using `add_host` module.

## Install servers

Once the cloud instance are created we will install the db-server and the web-servers using roles:

- db-server: role `prereq` will install all prerequisite and role `mysql` will install MySQL server & client and will setup the database to work with `simple-webapp`
- web-server: role `prereq` will install all prerequisite and role `flask` will install flask and setup the server along with the communication with the db-server.

## Configure traffic and load balancing

Then we will allow traffic for our cloud instances (80 for web server and 3306 for database server) using `gce_net` module. Load balancing will be configure to work with the web-servers using `gce_lb` module.

Then we'll send an email to our account to notify us that webserver is up and running, and that we can access it through the load balancer public ip.