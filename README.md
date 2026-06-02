# Red Hat 3scale API Management to Red Hat Connectivity Link migration tool

## Introduction

Questo repository contiene un playbook Ansible che permette di migrare automaticamente le configurazioni che trova su un'installazione di Red Hat 3scale API Management (3scale) verso un'installazione di Red Hat Connectivity Link (RHCL).

Il playbook non si occupa dell'installazione dell'operator di RHCL nè degli altri operatori richiesti. Inoltre, non si occupa neanche della configurazione iniziale di RHCL. Supporta però la configurazione degli oggetti di tipo Gateway.

## Prerequisites

Per usare il playbook è necessaria un'installazione di Ansible (per esempio, Red Hat Ansible Automation Platform); è fornito il file dei requirements qualora si optasse per la distribuzione di Ansible non supportata da Red Hat.

## Instructions

### Environment

Il playbook per funzionare ha bisogno del seguente ambiente:

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

Le varie chiavi hanno il seguente significato:
* `threescale.access_token`: è il token creato nella console di 3scale e che permette di interagire con le API di amministrazione di 3scale


```bash
ansible-playbook -e '{"threescale":{"access_token": "..."}}' main.yaml
```
