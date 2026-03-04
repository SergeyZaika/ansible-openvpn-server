# Ansible OpenVPN Server

An automated, reproducible VPN infrastructure for secure remote team access.

This project provides Ansible automation to deploy an OpenVPN server with PKI setup, NAT configuration, and automated client configuration generation — allowing teams to quickly bootstrap secure VPN access in a reproducible way.

## Requirements

- Ansible 2.9+
- Ubuntu 20.04 or 22.04 server
- Root or sudo access

## Description

This project automates the full lifecycle of an OpenVPN server: installation, PKI setup, firewall configuration, and client config generation — all in a single playbook run. A cleanup playbook is also included for teardown.

## Why Automate OpenVPN

Managing VPN infrastructure manually is error-prone and hard to reproduce. Automation solves this:

- **Repeatable infrastructure** — deploy identical servers every time
- **Fast disaster recovery** — rebuild the server in minutes, not hours
- **Easy client management** — generate client configs with one command
- **Reproducible deployments** — same result across environments
- **Infrastructure-as-code** — version-controlled, auditable, reviewable

## Architecture

```
           Internet
               |
       +---------------+
       |  OpenVPN      |
       |  Server       |
       |  (Ubuntu)     |
       +---------------+
          |         |
     VPN tunnel  VPN tunnel
          |         |
   +-----------+ +-----------+
   |  Client 1 | |  Client 2 |
   +-----------+ +-----------+
```

Traffic from VPN clients is routed through the server via an encrypted tunnel. The server handles NAT, routing, and certificate-based authentication.

## Project Structure

```
ansible-openvpn-server/
├── openvpn_setup.yaml
├── cleanup_openvpn.yaml
└── README.md
```

## Tested Environment

- Ubuntu 20.04
- Ubuntu 22.04
- Ansible 2.9+

## What This Project Demonstrates

- Infrastructure automation using Ansible
- Automated PKI generation with Easy-RSA
- OpenVPN server provisioning and configuration
- Firewall rules and NAT setup with iptables
- Client `.ovpn` configuration generation
- Idempotent infrastructure setup

## Playbooks

- **`openvpn_setup.yaml`** — Installs and configures the full OpenVPN server stack
- **`cleanup_openvpn.yaml`** — Removes all OpenVPN packages, configs, and firewall rules

## Usage

**Clone the repository:**

```bash
git clone https://github.com/SergeyZaika/ansible-openvpn-server
cd ansible-openvpn-server
```

**Adjust variables** in `openvpn_setup.yaml` if needed (server IP, client names, etc.).

**Run the setup playbook:**

```bash
ansible-playbook -i your_inventory_file openvpn_setup.yaml
```

This will:
- Install OpenVPN and Easy-RSA
- Generate CA, server, and client certificates
- Configure networking and firewall rules
- Create a ready-to-use `.ovpn` client configuration file

**To remove the server:**

```bash
ansible-playbook -i your_inventory_file cleanup_openvpn.yaml
```
