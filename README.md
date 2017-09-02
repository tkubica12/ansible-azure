# Ansible demo with Azure

Provision Azure infrastructure via Ansible and then configure VM to include Apache or NGINX.

## About this demo

It is showcase of imperative-model based desired state automation of Azure via Ansible Azure modules. It leverages modules for low lever work and error checking and focus on high level easy to read imperative infrastructure creation. During process created VMs are categorized into inventory and we then use declarative way (Ansible roles) to make those VMs contain Apache or NGINX.

## Install, setup

Follow Internet documentation to install Ansible and Azure Python SDK. Make sure you create Service Principal account in Azure (register application) and provide details either via environmental variables (example is in azurecredentials.rc.example), via ansible configuration file or any other method.

## How to run

ansible-playbook main.yaml

## Structure

Main Ansible playbook is main.yaml in root directory. This files defines input variables (list of desired VMs and their type - apache or nginx) and includes file web-servers.yaml than does infrastructure provisioning and then declaratively assign apache and nginx roles.

web-servers.yaml creates network and subnet if needed and than includes type-web-server.yaml for each VM defined in variables in main file.

type-web-server.yaml ensure VM provided as input variable exists, gather VM public IP address and add it into inventory and wait till server boots and starts responding to SSH.

Example includes two roles - apache and nginx. Those are located in roles directory and actual tasks are in tasks/main.yaml. Roles do install web server and wait until it responds on port 80.


Tomas Kubica
Find me on linkedin.com/in/tkubica

