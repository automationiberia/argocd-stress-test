# Argo CD Load Testing

This repository contains an Argo CD setup for load testing by deploying multiple instances of a customized guestbook application. Each instance serves unique content based on its configuration.

## Directory Structure

```plaintext
├── ansible.cfg
├── ansible-navigator.log
├── apps
│   └── helm-guestbook
│       ├── Chart.yaml
│       ├── guestbook-names.yaml
│       ├── templates
│       │   ├── deployment.yaml
│       │   ├── _helpers.tpl
│       │   ├── NOTES.txt
│       │   └── service.yaml
│       ├── values-production.yaml
│       └── values.yaml
├── bootstrap.yaml
├── collections
│   └── requirements.yaml
├── gitops
│   ├── bootstrap
│   │   └── applicationset-guestbooks-apps.yaml
│   └── installation
│       ├── argocd-app-bootstrap.yaml
│       ├── argocd-server.yaml
│       └── gitops-operator.yaml
├── group_vars
│   ├── all
│   │   └── main.yml
│   └── cluster1
│       └── vault.yaml
├── inventory
└── README.md
```
## Packages required

```
$  python3 -m pip install ansible-navigator --user
$  python3 -m pip install ansible-builder --user
```
## Populate and encrypt your credentials and custom data

```
$ vim group_vars/cluster1/vault.yaml
$ vim group_vars/all/main.yml
$ ansible-vault encrypt group_vars/*/vault.yaml
```
## Create OCP object needed to deploy Openshift GitOps and bootstrap the applications

```
$ ansible-navigator run bootstrap.yaml -i inventory -l cluster1 -m stdout --eei quay.io/automationiberia/ee-ocp-aap-iac-casc --vault-password-file .vault_password
```
## Variables

|Variable Name|Default Value|Required|Description|Example|
|:---|:---:|:---:|:---|:---|
|`ocp_api_key`|n/a|yes|Token used to authenticate with the Openshift API|'sha256~Po6ydC7CVs12drESQeNiUW9poUT84aFrj7zL3VQfvrS'|
|`ocp_api_host`|n/a|yes|Provide a URL for accessing the Openshift API|'=https://api.cluster-ocp.lab.example.com:6443'|
|`ocp_api_validate_certs`|false|no|Whether or not to verify the API server’s SSL certificates|'true'|
|`aws_access_key`|n/a|yes|Amazon Access Key to access AWS API|'R767AKIFYSF5INA6QKB6'|
|`aws_secret_key`|n/a|yes|Amazon Secret Key to access AWS API|'qKCYpd/jQX6gRhucQwIT1d2lzrapZ/O4lpEKGGqR'|
|`aws_region`|n/a|yes|Amazon region where the S3 will be deploy it|'us-central-3'|

