link: http://docs.openstack.org/developer/openstack-ansible/developer-docs/quickstart-aio.html#building-an-aio

Adjustments for translation checksite

1) in /opt/openstack-ansible/ansible-role-requirements.yml change the repo for os_horizon

- name: os_horizon
  scm: git
  src: https://github.com/eumel8/openstack-ansible-os_horizon
  version: 27cfd7d95a0f8e4bcbaa84bfa0493a355ec8453d

2) set public openstack service to http with
'echo "openstack_service_publicuri_proto: http" >> /etc/openstack_deploy/user_variables.yml'

3) Add a new set of variables in /etc/openstack_deploy/user_variables.yml

## translation checksite
zanata_url: https://translate.openstack.org:443
zanata_username: <user_name>
zanata_key: <user_api_key>
zanata_version: 3.8.1
translate_version: master
zanata_sync_hour: 18
zanata_sync_minute: 2


4) Start the regular AIO process

cd /opt/openstack-ansible

scripts/bootstrap-ansible.sh
scripts/bootstrap-aio.sh

cd playbooks

openstack-ansible setup-hosts.yml
openstack-ansible setup-infrastructure.yml
openstack-ansible setup-openstack.yml



