# Ansible OpenVPN Server

## Requirements
- Ansible 2.9+
- Ubuntu 20.04 or 22.04 server
- Root or sudo access

## Description
Infrastructure automation for deploying and cleaning up a single-node OpenVPN server on Ubuntu 20.04 and 22.04 using Ansible.

## Playbooks
- **openvpn_setup.yml**: Installs, configures, and finalizes the OpenVPN server setup.
- **cleanup_openvpn.yml**: Cleans up the OpenVPN server installation, removing all related packages, configurations, and rules.

## Usage

### Setup OpenVPN Server
1. Clone this repository.
2. Adjust variables in openvpn_setup.yaml if required.
3. Run the playbook:
   ```bash
   ansible-playbook -i your_inventory_file openvpn_setup.yml
