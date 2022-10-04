---
status: new
---

# Installere docker med script

Docker provides a convenience script at [get.docker.com](https://get.docker.com/) to install Docker into development environments quickly and non-interactively. The convenience script is not recommended for production environments, but can be used as an example to create a provisioning script that is tailored to your needs. Also refer to the [install using the repository](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository) steps to learn about installation steps to install using the package repository. The source code for the script is open source, and can be found in the [`docker-install` repository on GitHub](https://github.com/docker/docker-install).

- The script requires root or sudo privileges to run.
- The script attempts to detect your Linux distribution and version and configure your package management system for you, and does not allow you to customize most installation parameters.
- The script installs dependencies and recommendations without asking for confirmation. This may install a large number of packages, depending on the current configuration of your host machine.
- By default, the script installs the latest stable release of Docker, containerd, and runc. When using this script to provision a machine, this may result in unexpected major version upgrades of Docker. Always test (major) upgrades in a test environment before deploying to your production systems.
- The script is not designed to upgrade an existing Docker installation. When using the script to update an existing installation, dependencies may not be updated to the expected version, causing outdated versions to be used.

!!! note "Tip: preview script steps before running"

    You can run the script with the ``DRY_RUN=1`` option to learn what steps the script will execute during installation:
    ```bash
    curl -fsSL https://get.docker.com -o get-docker.sh
    DRY_RUN=1 sh ./get-docker.sh
    ```

This example downloads the script from [get.docker.com](https://get.docker.com/) and runs it to install the latest stable release of Docker on Linux:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```
