### Ansible Driven Rally Deployment for OpenStack Cloud Validation

#### About
This repository contains an Ansible playbook used to configure and install
a near complete Rally Benchmark Framework and Rally OpenStack Plugins inside
a Python virtual environment for ease of portability and re-usability. 

The motivation for this small project is to have a quickly reusable, isolated,
and up-to-date installation for Rally including all of the required components
to support the benchmarking or functionality testing of an OpenStack Cloud. 

This repository also contains a collection of Rally tasks in a single task file
that aims to be a close-to-complete functional validation of the most popular
components found in an OpenStack cloud: Keystone, Glance, Nova, Neutron, and Cinder.

Another motivation behind this was to use as a building block on how to set up Rally
once it has been deployed with the goal of understanding the overall workflow of
preparing a Rally environment to be ready to benchmark or test OpenStack deployments.



#### Requirements
* Red Hat based operating system. I used a Centos 8 virtual machine.
* Ansible 
* Git


#### Playbook variables

`rally_install_dir` - Rally installation directory. Contains the Python virtual environment directories, the Rally and Rally OpenStack plugins cloned from Github sources, as well as the sample Rally scenario task files.

`rally_config_dir` - This directory contains the minimal configuration of the rally.conf file. It is primarily used to specify a location for the sqlite database used by Rally to store target deployments and task result data in a persistent directory.

`rally_database_dir` - The path to the directory that will store the sqlite Rally database

`rally_venv_dir` - The directory of the virtual environment used 

`rally_gh_repos` - The git repository, branch, and destination directory for the cloned repository.

#### How to install

To run the playbook:

`ansible-playbook rally-deployment-setup.yaml`


#### How to use


