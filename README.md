# Ansible Learning Box

A hands-on Ansible playground with curated example playbooks, inventory, and configuration — designed to help learners practice common automation tasks (installing packages, managing services, using roles, and working with secrets).

## Highlights
- Beginner-friendly, well-commented example playbooks
- Inventory and config tuned for quick local/remote testing
- Examples of using roles and Ansible Vault (password file included for demos)
- Lightweight landing page to present the project visually

## Table of contents
- [What you'll learn](#what-youll-learn)
- [Repository layout](#repository-layout)
- [Prerequisites](#prerequisites)
- [Quick start](#quick-start)
- [Playbooks overview](#playbooks-overview)
- [Security & secrets](#security--secrets)
- [How to contribute](#how-to-contribute)
- [License & contact](#license--contact)

## What you'll learn
- Run Ansible playbooks against inventory hosts
- Install packages and services (apt, nginx, Docker)
- Structure simple roles and reuse them across playbooks
- Use Ansible Vault for secrets and supply vault password from a file
- Inspect and adapt variables, tasks, and inventory for real environments

## Repository layout
```
ansible.cfg                 # project-wide Ansible defaults (host_key_checking = False)
hosts.ini                   # example inventory with groups, SSH key path, and interpreter
playbooks/
  hello.yml                 # simple "hello" demo playbook using vars + command
  install_package.yml       # installs a list of packages using apt
  install_docker_with_role.yml  # example playbook that invokes a `docker` role
  setup_nginx.yml           # installs/configures nginx (demo)
  secrets.yml               # example secrets file (intended for vault)
  show_secrets.yml          # demo playbook to show how vault-protected variables can be used
  vault_password.txt        # demo vault password file (for learning only)
  index.html                # landing page for the learning box
  roles/                    # intended location for Ansible roles (community or custom)
```

How it fits together:
- `hosts.ini` defines the hosts and group variables (including the SSH key path and Python interpreter).
- `ansible.cfg` contains default behavior (host key checking disabled for convenience).
- `playbooks/` holds runnable examples; playbooks call roles or tasks that configure the remote systems.

## Prerequisites
- Ansible (2.9+ recommended, or a current stable release)
- Python 3 on controller and target (target interpreter referenced in inventory)
- SSH access to target hosts (private key path shown in `hosts.ini` — update it for your environment)
- Optional: Ansible Galaxy for role installation if you use community roles

## Quick start
Clone and run a playbook (replace inventory, key path and hosts with your values):
```bash
git clone https://github.com/phanivarun05/ansible-learning-box.git
cd ansible-learning-box

# Verify Ansible is installed
ansible --version

# Run the simple hello playbook
ansible-playbook -i hosts.ini playbooks/hello.yml

# Install packages demo
ansible-playbook -i hosts.ini playbooks/install_package.yml

# Run playbook that uses a role (ensure the role exists under playbooks/roles or install via ansible-galaxy)
ansible-playbook -i hosts.ini playbooks/install_docker_with_role.yml

# Run the nginx setup playbook
ansible-playbook -i hosts.ini playbooks/setup_nginx.yml

# If you want to use the provided vault password file (for demo only)
ansible-playbook -i hosts.ini playbooks/show_secrets.yml --vault-password-file=playbooks/vault_password.txt
```

Notes:
- Update `hosts.ini` to match your hosts and SSH key locations.
- `ansible.cfg` in the repo sets `host_key_checking = False` to avoid interactive prompts while learning; remove or change this for production environments.

## Playbooks — short descriptions
- playbooks/hello.yml  
  Minimal playbook demonstrating variables and a simple command task. Good first run to confirm connectivity.
- playbooks/install_package.yml  
  Installs a list of packages via apt and shows debug output for each item.
- playbooks/install_docker_with_role.yml  
  Example of calling a role (`docker`). Place your role in `playbooks/roles/docker` or install one via Ansible Galaxy.
- playbooks/setup_nginx.yml  
  Demonstrates installing and configuring nginx (service management, templates may be added).
- playbooks/secrets.yml & playbooks/show_secrets.yml  
  Demonstrate how sensitive data is referenced; intended to be used with Ansible Vault.
- playbooks/vault_password.txt  
  A demo vault password file included for learning; do NOT commit real passwords in production.

## Security & secrets (important)
- Do not store real secrets, credentials, or private keys in the repository. The included `vault_password.txt` and `secrets.yml` are for learning/demo purposes only.
- Use `ansible-vault encrypt` to protect variables and keep vault password files out of version control (or use an external secrets manager).
- The example `hosts.ini` references an SSH private key path. Replace this with the correct path on your controller or use an SSH agent.

## Suggestions for learners
- Edit `playbooks/hello.yml` to change variables and see templating in action.
- Build a `playbooks/roles/docker` role step-by-step: tasks/, handlers/, defaults/, templates/, and test it with `install_docker_with_role.yml`.
- Replace the plaintext `vault_password.txt` workflow with `ansible-vault` and CI-friendly secret storage.
- Add tests using `molecule` for roles and CI runs.

## How to contribute
- File a concise issue for bugs or improvement ideas.
- Prefer small, focused PRs: (1) add a role, (2) improve a playbook, (3) fix documentation/examples.
- Include a short explanation and testing steps with each PR.

## License & contact
- This project is provided for learning and experimentation. Add a LICENSE file (e.g., MIT) if you want to allow reuse.
- For questions or suggested examples to include, open an issue or create a pull request.

Enjoy learning Ansible — automate safely, iterate quickly, and have fun!
