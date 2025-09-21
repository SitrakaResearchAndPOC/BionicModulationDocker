# Testing docker compose for fm modulation on bionic
## Creating Dockerfile
```
nano Dockerfile
```
Tape ctrl+x + yes + enter
```
FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

# Step 1 : garder les dépôts en HTTP pour pouvoir installer ca-certificates
# (optionnel si sources.list contient déjà du HTTP)
RUN sed -i 's|https://archive.ubuntu.com|http://archive.ubuntu.com|g' /etc/apt/sources.list && \
    sed -i 's|https://security.ubuntu.com|http://security.ubuntu.com|g' /etc/apt/sources.list

# Step 2 : mise à jour initiale et installation des certificats
RUN apt-get update && apt-get install -y ca-certificates && apt-get clean && rm -rf /var/lib/apt/lists/*

# Step 3 : forcer maintenant HTTPS dans les sources
RUN sed -i 's|http://archive.ubuntu.com|https://archive.ubuntu.com|g' /etc/apt/sources.list && \
    sed -i 's|http://security.ubuntu.com|https://security.ubuntu.com|g' /etc/apt/sources.list

# Step 4 : mise à jour + installation complète
RUN apt-get update -o Acquire::Retries=5 -o Acquire::http::Timeout=30 && \
    apt-get install -y \
    gnuradio \
    hackrf \
    rtl-sdr \
    uhd-host \
    gr-osmosdr \
    ffmpeg \
    vlc \
    git \
    wget \
    unzip \
    nano \
    firefox \
    python3 \
    python3-pip && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Téléchargement des images UHD
RUN /usr/lib/uhd/utils/uhd_images_downloader.py || true

# Création utilisateur non-root
RUN useradd -ms /bin/bash user
USER user
WORKDIR /home/user

# Téléchargement projet FM Transmitter
RUN wget https://media.githubusercontent.com/media/SitrakaResearchAndPOC/fork_fm_transmitter/main/FM_Transmitter.zip && \
    unzip FM_Transmitter.zip && \
    rm FM_Transmitter.zip && \
    cd FM_Transmitter && \
    wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/BionicModulationDocker/refs/heads/main/emetteur-fm-uhd.grc

CMD ["/bin/bash"]
```
## Creating docker-compose.yml
```
nano docker-compose.yml
```
Tape ctrl+x + yes + enter

```
version: "3.8"

services:
  bionicmodulation:
    build: .
    container_name: bionicmodulation-fm
    privileged: true
    network_mode: host
    environment:
      DISPLAY: ${DISPLAY}
      LC_ALL: C.UTF-8
      LANG: C.UTF-8
    volumes:
      - /dev/bus/usb:/dev/bus/usb
      - /tmp/.X11-unix:/tmp/.X11-unix:ro
      - ${XAUTHORITY:-$HOME/.Xauthority}:/home/user/.Xauthority:ro
    stdin_open: true
    tty: true
```

## Launching 
```
docker-compose up -d
```
```
docker-compose ps
```
```
docker-compose exec bionicmodultion-fm
```
```
docker compose exec bionicmodulation uhd_usrp_probe
```
```
docker-compose exec bionicmodulation uhd_usrp_probe
```
```
docker-compose exec bionicmodulation gnuradio-companion
```
```
xhost +; docker-compose exec bionicmodulation gnuradio-companion
```
