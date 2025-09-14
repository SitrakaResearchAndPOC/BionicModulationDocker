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

