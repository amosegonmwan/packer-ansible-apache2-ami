# Packer and Ansible Setup for Apache2 Installation

## Description

This project involves creating a Packer template to build an Amazon Machine Image (AMI) that includes an Ansible provisioner to install Apache2. The setup is performed on an AWS Ubuntu EC2 instance with Ansible installed as the controller.

## Project Files

Create the following files in packer-build-dir:

- `ansible-playbook.yaml`
- `ubuntu-image.pkr.hcl`
- `variables.pkr.hcl`

### 1. `ansible-playbook.yaml`

This file contains the Ansible playbook that provisions the AMI by installing Apache2. It includes tasks for updating the package list, upgrading existing packages, and ensuring Apache2 is installed and updated to the latest version.

### 2. `ubuntu-image.pkr.hcl`

The Packer configuration file defines the source for creating the AMI, specifies the provisioners, and sets up the necessary post-processors. It uses the Amazon EBS source to create an Ubuntu-based AMI and includes an Ansible provisioner to apply the playbook defined in `ansible-playbook.yaml`.

### 3. `variables.pkr.hcl`

This file defines the variables used in the Packer template, including the region, AMI prefix, instance type, and tags. It provides default values and allows customization of the Packer build.

## Setup Instructions

### On Ansible Controller

1. **Install AWS CLI and Configure Access Keys**

   - Install `unzip`:
     ```bash
     sudo apt update
     sudo apt install unzip
     ```
   - Install the AWS CLI:
     ```bash
     curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
     unzip awscliv2.zip
     sudo ./aws/install
     ```
   - Configure AWS credentials:
     ```bash
     aws configure
     ```

2. **Install Packer on Ubuntu**

   - Add HashiCorp GPG Key:
     ```bash
     curl -fsSL https://apt.releases.hashicorp.com/gpg > hashicorp.gpg
     sudo mv hashicorp.gpg /etc/apt/trusted.gpg.d/
     ```
   - Add HashiCorp APT Repository:
     ```bash
     echo "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
     sudo apt update
     ```
   - Install Packer:
     ```bash
     sudo apt install packer
     packer version
     ```

### Project Directory Structure

1. Create a project directory `packer-build-dir` in `/home/ansible`:
   ```bash
   mkdir ~/packer-build-dir
   cd ~/packer-build-dir
   ```
2. Navigate to the Project Directory
   ```bash
   cd ~/packer-build-dir
   ```
3. Initialize, Format, Validate and Build the Packer Template
   ```bash
   packer init .
   packer fmt .
   packer validate .
   packer build .
   ```



