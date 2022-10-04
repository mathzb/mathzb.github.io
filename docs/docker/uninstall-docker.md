# Afinstallere Docker Engine

Uninstall the Docker Engine, CLI, Containerd, and Docker Compose packages:

```bash
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Images, containers, volumes, or customized configuration files on your host are not automatically removed. To delete all images, containers, and volumes:

```bash
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

!!! note

    You must delete any edited configuration files manually.
