# WSL2 DNS Update Script for Cisco AnyConnect VPN

<!-- markdownlint-disable MD013 -->
[![Shellcheck](https://github.com/zifamathebula/fix-wsl2-dns-resolution/workflows/Shellcheck/badge.svg?event=push)](https://github.com/zifamathebula/fix-wsl2-dns-resolution/actions?query=Shellcheck)
<!-- markdownlint-enable MD013 --> 
This script is designed to fix DNS resolution issues in WSL2 when using the Cisco AnyConnect VPN client in a full tunnel setup. It retrieves the DNS server entries from the local system and updates the `resolv.conf` file in WSL2. The script can be configured to run automatically on login/startup of the WSL2 instance.

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
