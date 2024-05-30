# Ansible

Use Ansible for configuration management and automation. Ansible is an open-source tool that simplifies the process of automating IT tasks such as software deployment, configuration management, and orchestration.

## Inventory

The inventory file (`inventories/setup.yml`) contains the list of hosts that Ansible manages. Currently, it includes the following host:

```yaml
all:
  hosts:
    your_name.organisation.cloud:
      ansible_host: IP_ADDRESS
      ansible_user: centos
```
The id_rsa private key is typically stored in the ~/.ssh directory on your local machine. Use the id_rsa private key to authenticate your SSH connection to the remote server (your_name.organisation.cloud), ensuring secure communication between our local machine and the server.

## Base Commands

### Running Playbook

To run the Ansible playbook (`playbook-app.yml`), use the following command:

```bash
ansible-playbook -i myproject/ansible/inventories/setup.yml playbook-app.yml
```

### SSH into Host
To SSH into the host (your_name.organisation.cloud), use the following command:

```bash
ssh centos@your_name.organisation.cloud
```