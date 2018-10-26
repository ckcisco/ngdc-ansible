# Deploy and configure siwapp

Deploy new VMs and configure them to run the siwapp inventory application. Deploy is written as its own ansible role so you may just make changes to that role for your environment without affecting the rest of the playbook.

The `deployment_environment` variable can be used to run a different set of tasks for different environments. Currently only the AWS deployment has been written.

At this time, only RedHat 7.5 has been tested.

## Overview

Ensure you've reviewed the variables for each role before running the playbook. There are variables in `group_vars` as well as in the `vars` folder for aws role.

The number of VMs deployed for the database tier and application tier is set by two variables in `group_vars`. We recommend deploying three because that is the configuration we've tested the most. The "web" tier is a single haproxy VM. The load balancer for the database tier is also a single haproxy VM.

## Deployment environments

### AWS EC2

We use the ansible module `ec2` to deploy instances. This module requires that you have the `boto` Python library installed.

### vCenter (planned)

TBD

## Tetration sensor install

To install the Tetration sensor for each tier, place one and only one RPM in the `/roles/tetration_sensor/files/` folder and set the appropriate variables as described below.

The following boolean variables define whether the Tetration sensor should be installed in each tier of the application.
* tet_sensor_db: the database tier
* tet_sensor_haproxydb : the haproxy for the database tier
* tet_sensor_application: the application tier
* tet_sensor_haproxyapp: the haproxy for the application tier (web)
* tet_sensor_loadsim: the load simulator tier

## More information

If you seek the answer to more of life's questions, reach out to this project's contributors:
* Doron Chosnek
* Brandon Beck