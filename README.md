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

Upon playbook completion there will be a post deployment message with information relevant to what are
the next steps to complete the Rally deployment. 

While the rest of these post-installation workflow tasks could be easily automated within Ansible, this
allows for users new to Rally to become familiar
on the procedure of creating a target deployment so that you can start running automated test cases against
your OpenStack cluster. Here are are the rest of the tasks required before you begin running automated test cases.

* Activate the virtual environment that was installed. This will give you access to the rally cli interface
* Source the `openrc` or OS_ environment files for the OpenStack deployment that will be imported as a target Rally environment for testing.
* Create the rally database: `rally db create`
* Create a rally deployment: `rally deployment create --fromenv --name <deployment name>`
* Test to ensure that Rally succesfully communicate with the OpenStack endpoints to the target test environment: `rally deployment check`


At this point Rally is installed, your target OpenStack environment that will be used for benchmark or validation testing is ready.
The next step is to configure and run the desired tasks. 

An example set of tasks have been provided in a file located in `{{ rally_config_dir }}/rally_configured_scenarios/rally-openstack-cloud-validation-task-example.yaml` - You can use that reference to explore the capabilities of the OpenStack plugins for Rally. 

The complete set of community provided sample scenarios can be found in `{{ rally_install_dir }}/rally_available_scenarios`

