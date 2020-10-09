### Ansible Driven Rally Benchmark Framework Deployment for OpenStack

#### About
This repository contains an Ansible playbook used to configure and install
a near complete Rally Benchmark Framework and Rally OpenStack Plugins inside
a Python virtual environment for ease of portability and re-usability. 

The motivation for this small project is to have a quickly reusable, isolated,
and up-to-date installation for Rally including all of the required components
to support the benchmarking or functionality testing of an OpenStack Cloud. 

This repository also contains a collection of Rally tasks in an example task file
that tryes to be a close-to-complete basic functional validation of the most popular
components found in an OpenStack cloud: Keystone, Glance, Nova, Neutron, and Cinder.

A complete list of supported OpenStack scenarios are available in the [Rally
OpenStack Plugin Repository.](https://github.com/openstack/rally-openstack/tree/master/samples)
These sample scenarios are also included as part of this installation in an easy to find location.

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

`rally_gh_repos` - The git repository, branch, and destination directory for the cloned repositories.

#### How to install

To run the playbook:

`ansible-playbook rally-deployment-setup.yaml`

#### How to use

Upon playbook completion there will be a post deployment message with relevant details for next steps  
to finalize your Rally deployment. 

While the rest of these post-installation workflow tasks can be easily automated within Ansible, this
allows for users new to Rally to become familiar
with the procedure of setting your first Rally environment running automated test cases against your OpenStack cluster
in a very short time. 

Here are are the rest of the tasks required before you begin running your first automated test case:

* Activate the python virtual environment where Rally was  installed by the playbook to access the Rally framework and plugins:  This will give you access to the rally cli interface. Example:
  * `source /opt/rally/rally_benchmark_environment/bin/activate`

* Create the rally database. This procedure is only performed only once: 
  * `rally db create`

* Source or activate the OpenStack environment file (`openrc`)  containing the authentication details of the target OpenStack cloud that you will be running benchmarks against:
  * `source /home/stack/overcloudrc`

* Create the first rally deployment using the OpenStack environment credentials source on the previous step: 
  * `rally deployment create --fromenv --name <deployment name>`

* Verify to ensure that Rally can successfully connect with the OpenStack endpoints of the target environment: 
  * `rally deployment check`


At this point Rally is installed, your target OpenStack environment that will be used for benchmark or validation testing is ready. The next step is to configure and run the desired tasks. 

An example set of tasks have been provided in a file located in `{{ rally_config_dir }}/rally_configured_scenarios/rally-openstack-cloud-validation-task-example.yaml` - You can use that reference to explore the capabilities of the OpenStack plugins for Rally. 

The complete set of community provided sample scenarios can be found in `{{ rally_install_dir }}/rally_available_scenarios`


The [Rally community documentation contains a quickstart guide](https://rally.readthedocs.io/en/latest/quick_start/tutorial/step_1_setting_up_env_and_running_benchmark_from_samples.html#running-rally-tasks) for getting started in running Rally tasks and its an excellent source of information as you explore the capabilities of this rather flexible and yet under utilized Opensource Utility.

