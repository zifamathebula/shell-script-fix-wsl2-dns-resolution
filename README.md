# Wsl2 DNS Update Script for Cisco AnyConnect VPN

<!-- markdownlint-disable MD013 -->
[![Shellcheck](https://github.com/zifamathebula/shell-script-fix-wsl2-dns-resolution/actions/workflows/shellcheck.yml/badge.svg)](https://github.com/zifamathebula/shell-script-fix-wsl2-dns-resolution/actions/workflows/shellcheck.yml)
[![Markdown Lint](https://github.com/zifamathebula/shell-script-fix-wsl2-dns-resolution/actions/workflows/markdownlint.yml/badge.svg)](https://github.com/zifamathebula/shell-script-fix-wsl2-dns-resolution/actions/workflows/markdownlint.yml)
This script is designed to fix DNS resolution issues in WSL2 when using the Cisco AnyConnect VPN client in a full tunnel setup. The issue arises because the automatic DNS configuration in WSL2 does not work properly when using the VPN. This prevents WSL2 from resolving addresses while the VPN connection is active.

## The Issue

When the Cisco AnyConnect VPN client is in a full tunnel setup, it sends all traffic over the VPN, including DNS requests. However, WSL2's automatic DNS configuration relies on the DNS servers configured in the Windows host. This configuration is not updated to match the DNS servers used by the VPN connection, causing DNS resolution to fail in WSL2.

The original GitHub issue describing the problem in detail can be found at the following link: [Issue Link](https://github.com/microsoft/WSL/issues/1350#issuecomment-844452775)

## The Solution

The script takes the following approach to resolve this issue:

1. It uses PowerShell commands to retrieve the current DNS server addresses from the local Windows system. This includes DNS servers from both the Cisco AnyConnect VPN adapter and other network adapters on the system.
2. The retrieved DNS server addresses are used to generate a new `resolv.conf` file in the specified WSL home directory. This file is used by WSL2 for DNS resolution.
3. The existing `resolv.conf` file in WSL2 is replaced with the newly generated one, allowing WSL2 to use the correct DNS servers.
4. Optionally, the script can be configured to run automatically on login/startup of the WSL2 instance. This ensures that the DNS configuration remains up-to-date as the VPN connects and disconnects.

By updating the `resolv.conf` file in WSL2 with the correct DNS server addresses, the script ensures that DNS resolution works properly while the VPN connection is active.

For more information on the solution, please refer to the following blog post: [Blog Post Link](https://www.frakkingsweet.com/automatic-dns-configuration-with-wsl-and-anyconnect-client/)

## How to use

1. Save the script as `wsl2-dns-update.sh` in your preferred directory.
2. Make the script executable by running `chmod +x wsl2-dns-update.sh`.
3. Run the script with `./wsl2-dns-update.sh`.
4. Follow the prompts to enter custom values for the WSL home directory, PowerShell path, and DNS configuration path, or press Enter to use the default values.
5. When prompted, enter "y" (or "Y") to add the script to the startup scripts for your WSL2 instance.

## How it works

1. The script retrieves the current DNS server addresses from the local system using PowerShell commands.
2. The DNS server addresses are then used to generate a new `resolv.conf` file in the specified WSL home directory.
3. The existing `resolv.conf` file in WSL2 is replaced with the newly generated one.
4. If the user chooses to add the script to the startup scripts, it creates a `wsl-startup.sh` script in the user's home directory (if it doesn't already exist) and adds the DNS update function to it.
5. The `wsl-startup.sh` script is then added to the `.bashrc` file to be executed on login/startup of the WSL2 instance.

## Troubleshooting

If you experience issues with the script, check the following:

1. Ensure the script has the correct permissions by running `chmod +x wsl2-dns-update.sh`.
2. Make sure the paths to the WSL home directory, PowerShell, and the DNS configuration file are correct.
3. Verify that your VPN connection is working properly.

If you still have issues, refer to the original [Github issue](https://github.com/microsoft/WSL/issues/1350#issuecomment-844452775) for more information and potential solutions.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE.txt) file for details.

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests to help improve this script.

1. Fork the repository.
2. Create a new branch with a descriptive name.
3. Make your changes and commit them to the new branch.
4. Submit a pull request with your changes.

## Buy Me a Coffee

If you find this script useful and would like to show your appreciation, you can buy me a coffee:

[![Buy Me a Coffee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/zifamathebula)
<!-- markdownlint-enable MD013 -->
