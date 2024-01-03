# AlmaLinux 9.3 ISO Download and SHA256 Verification Playbook

## Overview
This Ansible playbook automates the downloading of the AlmaLinux 9.3 ISO file and verifies its integrity using SHA256 checksum. It's designed to ensure the authenticity and integrity of the downloaded ISO file.

## Requirements
- Ansible installed on the host machine.
- Sufficient storage space for the ISO file.
- Internet connectivity for downloading the ISO file.

## How It Works
1. **Download Task**: The playbook downloads the AlmaLinux 9.3 ISO file from the specified URL to a designated directory on the local system.
2. **SHA256 Checksum Verification**: After the download completes, the playbook verifies the ISO file's SHA256 checksum to ensure the file's integrity.

## Variables
- `iso_url`: The URL of the AlmaLinux 9.3 ISO file.
- `destination`: The local path where the ISO file will be saved.
- `expected_sha256`: The expected SHA256 checksum of the ISO file.

## Usage
1. Ensure Ansible is installed on your machine.
2. Configure the playbook variables (`iso_url`, `destination`, and `expected_sha256`) as needed.
3. Run the playbook using the following command:

   ```bash
   ansible-playbook download-verify-almalinux-iso.yml
   ```

## Playbook Structure
The playbook consists of the following main tasks:

- **Download AlmaLinux ISO**: Downloads the ISO file asynchronously.
- **Wait for the download to complete**: Checks the download status until completion.
- **Verify SHA256 Checksum**: Compares the calculated checksum of the downloaded file with the expected checksum.
- **Display Checksum Verification Result**: Outputs the result of the checksum verification.

## Troubleshooting
- If the download or checksum verification fails, check the `expected_sha256` variable to ensure it matches the checksum of the ISO file.
- Ensure that the specified `destination` directory exists and has adequate space for the ISO file.

## Author
Johan Sörell | [GitHub](https://github.com/J-SirL)

## License
This project is licensed under the GNU General Public License v3.0. For more details, see the [GPLv3 License](https://www.gnu.org/licenses/gpl-3.0.en.html).
