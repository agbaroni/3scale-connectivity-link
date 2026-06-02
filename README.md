# Red Hat 3scale API Management to Red Hat Connectivity Link migration tool

## Introduction

This repository contains an Ansible playbook that allows you to automatically migrate configurations found on a Red Hat 3scale API Management (3scale) installation to a Red Hat Connectivity Link (RHCL) installation.

The playbook does not handle the installation of the RHCL operator or its required prerequisite operators. Furthermore, it does not cover the initial configuration of RHCL. However, it does support the configuration of Gateway objects.

## Prerequisites

To use the playbook, an Ansible installation is required (such as Red Hat Ansible Automation Platform); a requirements file is provided in case you opt for an Ansible distribution not supported by Red Hat.

## Instructions

### Environment

The playbook requires the following environment to run:

```yaml
threescale:
  access_token: <3SCALE ACCESS TOKEN>
  products:
    - name: <PRODUCT NAME>
      enabled: true
      service:
        name: <BACKEND SERVICE NAME>
  hostname: <3SCALE HOSTNAME>

connectivity_link:
  gateway:
    class_name: <GATEWAY CLASS NAME>
    cluster_issuer: <GATEWAY CLUSTER ISSUER>
    domain:
      base: <CL BASE DOMAIN>
    name: <GATEWAY NAME>
    project:
      display_name: <GATEWAY NAMESPACE DISPLAY NAME>
      name: <GATEWAY NAMESPACE NAME>
  apis:
    - name: <API NAME>
      project: <API NAMESPACE NAME>
```

The keys have the following meanings:
* `threescale.access_token`: This is the token created in the 3scale console that allows interaction with the 3scale administration APIs; as we will see, the value of this key is usually specified on the Ansible command line.
* `threescale.products[*].name`: The name of a Product as indicated within 3scale.
* `threescale.products[*].enabled`: If `false`, the Product is ignored.
* `threescale.products[*].service.name`: The name of the Kubernetes `Service` that exposes the software component.
* `threescale.hostname`: The hostname of the 3scale console Route.
* `connectivity_link.gateway.class_name`: The name of `GatewayClass`
* `connectivity_link.gateway.cluster_issuer`: The name of the `ClusterIssuer` used to create the certificates for the `Gateway`.
* `connectivity_link.gateway.domain.base`: The common part of the URL where all the APIs defined in RHCL for this `Gateway` will be exposed.
* `connectivity_link.gateway.name`: The name of `Gateway` instance.
* `connectivity_link.gateway.project.name`: The name of the `Project` where the `Gateway` instance is located.
* `connectivity_link.gatewat.project.display_name`: The friendly name of the `Project` where the `Gateway` instance is located.
* `connectivity_link.apis[*].name`: The name of an API exposed by RHCL.
* `connectivity_link.apis[*].project`: The name of the `Project` where the API exposed by RHCL is configured.

### Execution

To run the playbook, execute the following command:

```bash
ansible-playbook -e '{"threescale":{"access_token": "..."}}' main.yaml
```
