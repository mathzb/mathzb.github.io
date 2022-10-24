```yaml
version: "3"
services:
  NginxProxyManager:
    image: "jc21/nginx-proxy-manager:latest"
    container_name: NginxProxyManager
    restart: unless-stopped
    ports:
      - "80:80"
      - "81:81"
      - "443:443"
    environment:
      - DB_MYSQL_HOST=db.baungrd.dk
      - DB_MYSQL_PORT=3306
      - DB_MYSQL_USER=npm
      - DB_MYSQL_PASSWORD=PASSWORD
      - DB_MYSQL_NAME=npm
      - DISABLE_IPV6=true
    volumes:
      - /home/mathzb/docker/npm/data:/data
      - /home/mathzb/docker/npm/letsencrypt:/etc/letsencrypt

  teamspeak:
    image: "mbentley/teamspeak"
    container_name: teamspeak
    restart: unless-stopped
    ports:
      - "9987:9987/udp"
      - "30033:30033"
      - "10011:10011"
      - "41144:41144"
    environment:
      - PUID=1000
      - PGID=1000
      - TS3SERVER_GDPR_SAVE=false
      - TS3SERVER_LICENSE=accept
      - serveradmin_password=PASSWORD
    volumes:
      - /home/mathzb/docker/teamspeak/data:/data

  vaultwarden:
    image: "vaultwarden/server:latest"
    container_name: vaultwarden
    restart: unless-stopped
    ports:
      - "8081:80"
    environment:
      - ADMIN_TOKEN=
      - WEBSOCKET_ENABLED=true
      - DATABASE_URL=mysql://vaultwarden:PASSWORD@db.baungrd.dk:3306/vaultwarden
    volumes:
      - /home/mathzb/docker/vaultwarden:/data

  plex:
    image: lscr.io/linuxserver/plex:latest
    container_name: plex
    network_mode: host
    environment:
      - PUID=1000
      - PGID=1000
      - VERSION=docker
      - PLEX_CLAIM=
    volumes:
      - "/home/mathzb/docker/plex:/config"
      - "/home/mathzb:/storage:rw"
      - "/home/mathzb/docker/xteve/data:/epg:rw"
    restart: unless-stopped

  deluge:
    image: lscr.io/linuxserver/deluge:latest
    container_name: deluge
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Copenhagen
      - DELUGE_LOGLEVEL=error #optional
    volumes:
      - /home/mathzb/docker/deluge:/config
      - /home/mathzb/downloads:/downloads
    ports:
      - 8112:8112
      - 6881:6881
      - 6881:6881/udp
    restart: unless-stopped

  filebot:
    container_name: filebot
    image: jlesage/filebot
    ports:
      - "5800:5800"
    environment:
      - USER_ID=1000
      - GROUP_ID=1000
      - AMC_ACTION=symlink
      - AMC_SERIES_FORMAT={plex}
      - AMC_MOVIE_FORMAT={plex}
      - AMC_INPUT_DIR=/storage/downloads
      - AMC_OUTPUT_DIR=/storage/FileBot-Media
    volumes:
      - "/home/mathzb/docker/filebot:/config:rw"
      - "/home/mathzb:/storage:rw"
      - "/home/mathzb/downloads:/watch:rw"
      - "/home/mathzb/FileBot-Media:/output:rw"
    restart: unless-stopped

  portainer:
    container_name: portainer
    image: portainer/portainer-ce:2.15.0
    ports:
      - "8000:8000"
      - "9443:9443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /home/mathzb/docker/portainer:/data
    restart: unless-stopped

  phpmyadmin:
    image: lscr.io/linuxserver/phpmyadmin:latest
    container_name: phpmyadmin
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Copenhagen
      - PMA_ARBITRARY=1 #optional
      - PMA_ABSOLUTE_URI=http://sql.baungrd.dk #optional
    volumes:
      - /home/mathzb/docker/phpmyadmin/config:/config
    ports:
      - 8880:80
    restart: unless-stopped

  unifi-controller:
    image: lscr.io/linuxserver/unifi-controller:latest
    container_name: unifi-controller
    environment:
      - PUID=1000
      - PGID=1000
    volumes:
      - /home/mathzb/docker/unifi:/config
    ports:
      - 8443:8443
      - 3478:3478/udp
      - 10001:10001/udp
      - 8080:8080
      - 8843:8843 #optional
      - 8881:8880 #optional
      - 6789:6789 #optional
      - 5514:5514/udp #optional
    restart: unless-stopped
```
