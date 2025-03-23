# terraform-ansible-workshop
 
This project demonstrates the use of Terraform and Ansible to provision and configure infrastructure. The setup includes provisioning servers and configuring them with Apache and NGINX using Ansible playbooks.

## Project Structure

```
ansible-nginx/
├── ansible.cfg
├── inventories/
│   ├── production/
│   │   └── hosts
│   └── staging/
│       └── hosts
├── playbooks/
│   └── install_nginx.yml
│   └── install_apache.yml
├── roles/
│   └── nginx/
│       ├── defaults/
│       │   └── main.yml
│       ├── tasks/
│       │   └── main.yml
│       └── templates/
│           └── nginx.conf.j2
│    └── apache/
│       ├── defaults/
│       │   └── main.yml
│       ├── tasks/
│       │   └── main.yml
│       └── templates/
│           └── apache.conf.j2
└── vars/
    └──  development.yml
    └──  staging.yml
```

## Prerequisites

- Terraform
- Ansible
- SSH key pair (`tf-cloud-init` and `tf-cloud-init.pub`)
- Two EC2 instances created using the [terraform-workshop](https://github.com/ronaldorodriguezbermudez/terraform-workshop) repository

## Setup

1. Clone the repository:
    ```sh
    git clone https://github.com/ronaldorodriguezbermudez/terraform-ansible-workshop.git
    cd terraform-ansible-workshop
    ```

2. Ensure you have the necessary SSH keys in place:
    - `tf-cloud-init`
    - `tf-cloud-init.pub`

    Use the same keys created in the [terraform-workshop](https://github.com/ronaldorodriguezbermudez/terraform-workshop) project.

3. Update the inventory files with your server details:
    - `inventories/development/hosts`
    - `inventories/staging/hosts`
    
     Replace the public IPs in the inventory files with the public IPs of your EC2 instances.


4. Update the variable files with the appropriate package versions:
    - `vars/development.yml`
    - `vars/staging.yml`

## Usage

### Configuring Servers

Use Ansible to configure the servers. Replace `env` with either `development` or `staging`.

#### Install Apache (Staging)

In the staging environment, Apache is installed and configured.

```sh
ansible-playbook -i inventories/staging/hosts install_apache.yml -e "env=staging"
```

#### Install NGINX (Development)

In the development environment, NGINX is installed and configured.

```sh
ansible-playbook -i inventories/development/hosts install_nginx.yml -e "env=development"
```

## Configuration Files

### Ansible Configuration

The `ansible.cfg` file contains the Ansible configuration settings.

### Inventory Files

The inventory files are located in the `inventories` directory and contain the server details for different environments.

### Playbooks

The playbooks for installing Apache and NGINX are located in the `playbooks` directory.

### Roles

The roles for configuring Apache and NGINX are located in the `roles` directory.

### Variables

The variable files for different environments are located in the `vars` directory.

## Acknowledgements

This project was created using the [terraform-workshop](https://github.com/falconcr/terraform-workshop) repository as a guide and the guidance of [Gerardo López](https://www.linkedin.com/in/gerardo-falcon)