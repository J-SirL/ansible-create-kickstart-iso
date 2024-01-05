## Ansible Role: Create Kickstart ISO

### Author
Johan Sörell  
GitHub: [J-SirL](https://github.com/J-SirL/)

### Table of Contents
1. [Overview](#overview)
2. [Directory Structure](#directory-structure)
3. [Default variables](#default-variables)
4. [Usage](#usage)
5. [Example Playbook](#example-playbook)
6. [Requirements File](#requirements-file-requirementsyml)
7. [Kickstart Files](#kickstart-files)
   - [server-ks.cfg.j2](#server-kscfgj2)
   - [workstation-ks.cfg.j2](#workstation-kscfgj2)

### Overview
This Ansible role, created by Johan Sörell, is designed for creating a Kickstart ISO, particularly for AlmaLinux 9. It automates the process of downloading an ISO, applying custom configurations, and generating a new ISO with Kickstart settings.

### Directory Structure
```bash
ansible-create-kickstart-iso/
├── defaults
│   └── main.yml
├── documentation
│   ├── HowTo_use_encrypted_password_in_kickstart.md
│   ├── server-ks.cfg.j2.md
│   └── workstation-ks.cgf.j2.md
├── LICENSE
├── meta
│   └── main.yml
├── README.md
├── site.yml
├── tasks
│   ├── check_iso_status.yml
│   ├── create_kickstart_iso.yml
│   ├── download-almalinux-9.yml
│   └── main.yml
└── templates
    ├── config
    │   ├── server-ks.cfg.j2
    │   └── workstation-ks.cfg.j2
    ├── grub.cfg.j2
    └── isolinux.cfg.j2
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

### Default Variables

This section details the default variables defined in the `defaults/main.yml` file of the role, explaining their purpose and usage:

- **`ks_pass`**
  - **Value**: `$6$jpVj9WymVzsOZVBX$SIxH/SA/LaEtFacGtjwb72680RgYSuYznwv8Yu9zgQgJCpcw3BOu85JVIXwUBYDP/DErpnS3fwAb4QuuyV1ag1`
  - **Description**: The encrypted password used in the Kickstart configuration.
  - **Usage**: Utilized for setting up user accounts within the Kickstart files.
  - You need to change the password to be able to use your system I have written a HowTo Guide if you do not know how to do that. [HowTo use encrypted password in kickstart](documentation/HowTo_use_encrypted_password_in_kickstart.md)

- **`kickstart_type`**
  - **Value**: `workstation` (valid options are `server` or `workstation`)
  - **Description**: Specifies the type of installation.
  - **Usage**: Determines which Kickstart configuration template is used for generating the ISO.

- **`ks_new_iso_path`**
  - **Value**: `"{{ playbook_dir }}/finished_iso/"`
  - **Description**: The path where the newly created Kickstart ISO will be stored.
  - **Usage**: Defines the output location for the generated ISO file.

- **`ks_original_iso_dir`**
  - **Value**: `"{{ playbook_dir }}/original_iso"`
  - **Description**: Directory to store the original ISO file.
  - **Usage**: Acts as a storage location for the original, unmodified ISO.

- **`ks_original_iso_path`**
  - **Value**: `"{{ ks_original_iso_dir }}/AlmaLinux-9.3-x86_64-dvd.iso"`
  - **Description**: The path to the original AlmaLinux ISO file.
  - **Usage**: Specifies the location of the ISO file to be used as the base for modifications.

- **`ks_working_directory`**
  - **Value**: `"/tmp/isowork"`
  - **Description**: Temporary working directory used during ISO creation.
  - **Usage**: Serves as a workspace for processing and generating the Kickstart ISO.

- **`ks_iso_url`**
  - **Value**: `"https://repo.almalinux.org/almalinux/9.3/isos/x86_64/AlmaLinux-9.3-x86_64-dvd.iso"`
  - **Description**: URL to download the AlmaLinux ISO.
  - **Usage**: Used for downloading the ISO file if it’s not already present in the specified directory.

- **`ks_expected_sha256_checksum`**
  - **Value**: `"a8c4ed4b79edd0977d7f88be7c07e12c4b748671a7786eb636c6700e58068d5"`
  - **Description**: SHA256 checksum for the downloaded ISO for verification.
  - **Usage**: Ensures the integrity and authenticity of the downloaded ISO file.

These default variables provide current configuration options for the role, enabling customization and flexibility in how the Kickstart ISO is created and customized.

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
[workstation-ks.cfg.j2](documentation/workstation-ks.cgf.j2.md)
