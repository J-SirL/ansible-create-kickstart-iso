# AlmaLinux 9 ISO Repackaging with Ansible

## Author
Johan Sörell - [GitHub](https://github.com/J-SirL)

## Overview

This documentation outlines an Ansible playbook designed to automate the process of unpacking an AlmaLinux 9 ISO, reconfiguring it for Kickstart, and then repackaging it into a new ISO file.

### Main Tasks
1. Install necessary packages for ISO manipulation.
2. Create working directories for ISO mounting and manipulation.
3. Mount the original AlmaLinux ISO.
4. Copy the contents from the ISO to a working directory.
5. Unmount the ISO.
6. Add a custom Kickstart file to the working directory.
7. Update the boot configuration to use the Kickstart file.
8. Recreate the ISO with the new settings.
9. Add an MD5 checksum to the new ISO.
10. Cleanup the working directory.

### Prerequisites

- Ansible installed on the control node.
- Sufficient permissions to mount and unmount file systems, and to run the required commands.
- Paths to the original ISO, the new ISO, and the Kickstart file.

### Playbook Variables

- `original_iso_path`: Path to the original AlmaLinux ISO.
- `new_iso_path`: Path where the new ISO will be saved.
- `ks_file_path`: Path to the Kickstart file.
- `working_directory`: Temporary working directory path.

### Playbook Execution

Run the playbook using the Ansible command:

```bash
ansible-playbook almalinux_iso_repackage.yml
```

### Playbook Content

```yaml
---
- name: AlmaLinux 9 ISO Repackaging
  hosts: localhost
  become: yes
  vars:
    original_iso_path: "/path/to/original/almalinux.iso"
    new_iso_path: "/path/to/new/almalinux.iso"
    ks_file_path: "/path/to/ks.cfg"
    working_directory: "/tmp/isowork"

  tasks:
    # ... (Playbook tasks here) ...
```

### Note

- Replace variable paths with actual paths in your environment.
- Ensure the `ks.cfg` file is properly formatted and located at the specified path.
- Run this playbook in a controlled environment before using it in production.

---

This document, authored by Johan Sörell, provides a concise guide on using the provided Ansible playbook for repackaging an AlmaLinux 9 ISO with custom Kickstart settings.