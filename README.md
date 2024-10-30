# Argo CD Load Testing

This repository contains an Argo CD setup for phased load testing by deploying multiple instances of a customized Nginx application. Each instance serves unique content based on its configuration.

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
