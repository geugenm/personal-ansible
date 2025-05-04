# personal-ansible

A minimal, cross-platform Ansible configuration for provisioning personal development environments. Zero garbage, maximum efficiency.

## Overview

This repository contains Ansible playbooks and roles for managing both Linux and Windows machines in a personal development setup. Optimized for C++/Python development environments with sensible defaults that don't waste your time.

```
personal-ansible/
├── inventory/
│   ├── hosts.yml           # Host definitions
│   └── group_vars/         # Variables by host group
├── roles/
│   ├── common/             # Base configuration for all systems
│   ├── dev-tools/          # Development tools configuration
│   ├── oh-my-zsh/          # Terminal setup for Linux
│   └── windows-config/     # Windows-specific configuration
├── playbooks/
│   ├── linux.yml           # Linux-specific playbook
│   ├── windows.yml         # Windows-specific playbook
│   └── site.yml            # Main playbook
└── readme.md               # This file
```

## Features

- Cross-platform support for Linux and Windows environments
- Minimal configuration with maximum impact
- Shell environment optimization (Oh My Zsh on Linux)
- Dev tooling setup (C++, Python, build tools)
- Error-resilient idempotent operations

## Requirements

### Control Node (Linux)

- Ansible 2.13+
- Python 3.9+

### Managed Nodes

- **Linux**: SSH access with sudo privileges
- **Windows**: WinRM configured (see setup instructions below)

## Windows Support

Windows can only be used as a managed node, not as a control node. Configuration is done via WinRM:

```bash
# Run this on Windows nodes (PowerShell as Administrator)
$url = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
$file = "$env:temp\ConfigureRemotingForAnsible.ps1"
(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)
powershell.exe -ExecutionPolicy ByPass -File $file
```

## Usage

Clone and run:

```bash
# Clone repository
git clone https://github.com/geugenm/personal-ansible.git
cd personal-ansible

# Edit inventory/hosts.yml to match your environment

# Run on all hosts
ansible-playbook -i inventory/hosts.yml playbooks/site.yml

# Run on specific host
ansible-playbook -i inventory/hosts.yml playbooks/site.yml --limit workstation

# Run specific tags
ansible-playbook -i inventory/hosts.yml playbooks/site.yml --tags "dev,shell"
```

## Testing and Validation

```bash
# Syntax check
ansible-playbook playbooks/site.yml --syntax-check

# Dry run
ansible-playbook -i inventory/hosts.yml playbooks/site.yml --check
```

## License

MIT. Do whatever you want with it.
