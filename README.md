# ONOS Form Cluster Docker Image
This contains the files to construct a docker image around the onos-form-cluster utility script. The docker entry point looks for an
environment variable (`CLUSTER_HOSTS`) and waits for each of the ONOS instances specified to respond to their REST interface (`http://host:8181/onos/v1/cluster`). After all hosts have responded to their REST interface the script then pushes the appropriate cluster configuration to each ONOS instance.

This docker image is meant for usage in a docker-compose file so that the compose can form a cluster after all the ONOS instance are specified.

## links
It is important that not only the `CLUSTER_HOSTS` environment variable is set, but also that each ONOS instance is also linked from this container as well (see docker-compose example below).

## Docker Compose
A sample docker-compose entry for this container
```
form_cluster:
  image: ciena/onos-form-cluster
  container_name: form_cluster
  environment:
    CLUSTER_HOSTS: controller_1,controller_2,controller_3
  links:
    - controller_1
    - controller_2
    - controller_3
  labels:
      org.onlabs.cord.name: onos-form-cluster
      org.onlabs.cord.type: utility
  restart: never
```
