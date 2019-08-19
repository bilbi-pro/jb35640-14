
Homework:
the grand hotel, decided to migrate their entire application infrastractur to be containered base.
but before starting the migrations, the IT manager, asks you to build appropriate infrastracture for the new infrastracture.
for now we need to handle the metric collection part of the infrastractures.

here you will need to build virtual machine (centos based), and install the docker engine, and all appropriate components that will enable proper metrics collections for the containers.

please don't forget:
* remember the technics\utilities to expose the docker engine metrics
*

Tasks:

1. on the VM, install the docker engine, using the appropriate repository manager (yum)
2. configure the docker engine, to expose both metrics and managment port, use the following config, remeber the path of the docker engine config files.
```json
{
"metrics-addr" : "0.0.0.0:9323",
"experimental" : true
}
```
