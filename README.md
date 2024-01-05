## Ansible Role: Create Kickstart ISO

### Author
Johan Sörell  
GitHub: [J-SirL](https://github.com/J-SirL/)

### Table of Contents
1. [Overview](#overview)
2. [Directory Structure](#directory-structure)
3. [Key Components](#key-components)
   - [Tasks](#tasks)
   - [Templates](#templates)
   - [Defaults](#defaults-mainyml)
   - [Meta](#meta-mainyml)
5. [Usage](#usage)
6. [Example Playbook](#example-playbook)
7. [Requirements File](#requirements-file-requirementsyml)
8. [Kickstart Files](#kickstart-files)
   - [server-ks.cfg.j2](#server-kscfgj2)
   - [workstation-ks.cfg.j2](#workstation-kscfgj2)

### Overview
This Ansible role, created by Johan Sörell, is designed for creating a Kickstart ISO, particularly for AlmaLinux 9. It automates the process of downloading an ISO, applying custom configurations, and generating a new ISO with Kickstart settings.

### Directory Structure
- **tasks**: Contains the YAML files for tasks.
- **templates**: Jinja2 templates for configuration files.
- **defaults**: Default variables for the role.
- **meta**: Metadata about the role.

### Key Components

#### Tasks
1. **main.yml**
   ```yaml
   {content of tasks/main.yml}
   ```
2. **Other Task Files**
   - `check_iso_status.yml`: 
     ```yaml
     {content of tasks/check_iso_status.yml}
     ```
   - `create_kickstart_iso.yml`: 
     ```yaml
     {content of tasks/create_kickstart_iso.yml}
     ```
   - `download-almalinux-9.yml`: 
     ```yaml
     {content of tasks/download-almalinux-9.yml}
     ```

#### Templates
- **grub.cfg.j2**
  ```jinja2
  {content of templates/grub.cfg.j2}
  ```
- **isolinux.cfg.j2**
  ```jinja2
  {content of templates/isolinux.cfg.j2}
  ```
- **server-ks.cfg.j2**
  This Jinja2 template is for a server-based Kickstart configuration. It includes settings for graphical installation, repository setup, kdump configuration, localization, network setup, package selection, disk configuration, timezone, and user settings. It's dynamically generated using Ansible variables, providing flexibility for customization.
  ```jinja2
  # Full content and detailed explanation of server-ks.cfg.j2
  {full content of server-ks.cfg.j2}
  ```
- **workstation-ks.cfg.j2**
  This Jinja2 template is used for creating a workstation-based Kickstart configuration for AlmaLinux installations. It includes a variety of settings specific to a workstation setup, such as package selection, disk partitioning, network configuration, and user account settings.
  ```jinja2
  # Full content and detailed explanation of workstation-ks.cfg.j2
  {full content of workstation-ks.cfg.j2}
  ```

#### Defaults (main.yml)
```yaml
{content of defaults/main.yml}
```

#### Meta (main.yml)
```yaml
{content of meta/main.yml}
```

### Usage
Include this role in your Ansible playbook to facilitate the creation of a Kickstart ISO. Customize the default variables and templates as needed to suit your specific requirements.

### Example Playbook
```yaml
---
- name: Install role JsirL create_kickstart_iso
  hosts: localhost
  connection: local
  become: true
  roles:
    - role: JsirL.create_kickstart_iso
```

### Requirements File (`requirements.yml`)
```yaml
---
roles: 
  - name: JsirL.create_kickstart_iso
    src: git@github.com:J-SirL/ansible-create-kickstart-iso
    scm: git
    version: main
```

### Kickstart Files
#### server-ks.cfg.j2

Documentation is of server-ks-cfg is located under documentation/server-ks.cfg.j2.md
[server-ks.cfg.j2](documentation/server-ks.cfg.j2.md)


#### workstation-ks.cfg.j2

Documentation is of server-ks-cfg is located under documentation/server-ks.cfg.j2.md
[workstation-ks.cfg.j2](documentation/workstation-ks.cfg.j2.md)
