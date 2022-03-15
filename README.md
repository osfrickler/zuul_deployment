# Zuul-CI deployment

This repository contains the OSISM Zuul-CI installation setup.
Zuul-CI is a gating system which goes beyond normal CI-CD pipeline functionality.


## How to add a repository

If you want to add your repository to zuul, you also have to create a PR in here.
The file to touch is *main.yml*. In the playbooks **role** section
you'll find a single role. From there, go to
```yaml
vars.tenants[0].tenant.source.githubzuulapp.untrusted-projects
```
and add your repository in here. Preferably in alphabetical order.
Once the PR is approved, it'll take only a few minutes until your repo is available in zuul.


## Setup

Installation steps


### Github App

In oder to have Zuul-CI working with GitHub you need to setup a GitHub app.
A guide on how to setup this app can be found here:
https://github.com/tibeerorg/zuul_setup


### Infrastructure as Code (IaC)

To deploy a new Zuul server, edit the variables at the beginning of
``deploy.yml`` according to your setup and then call:

```bash
ANSIBLE_ROLES_PATH=../infrastructure ansible-playbook deploy.yml
```


### Provisioning

Done via Ansible. TODO: Automatically performed on changes in main branch.
```bash
ansible-playbook --extra-vars "webhook_token=webhooksecretvalue db_user_pass=userpassword db_root_pass=rootpassword" main.yaml
```

or

```bash
ANSIBLE_ROLES_PATH=../infrastructure:../ansible-collection-services/roles ansible-playbook -e @vars.yml --vault-pass-file .ansible_pass main.yaml
```

TODO: Install ansible collection, adopt ansible config. Describe setting up files (clouds.yaml + nodepool{,.pub})

## License

Apache License 2.0
