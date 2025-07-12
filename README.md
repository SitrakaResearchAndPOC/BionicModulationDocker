# BionicModulationDocker
# INSTALLATION OF MODULATION
## PREPARING IMAGE
```
xhost +
```
```
docker image pull ubuntu:18.04
```
```
docker run -tid --privileged -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro --net=host --env="DISPLAY=$DISPLAY" --env="LC_ALL=C.UTF-8" --env="LANG=C.UTF-8" --name bionicmodulation ubuntu:18.04
```
```
docker exec -ti bionicmodulation /bin/bash
```
```
apt update
```
```
apt install nano firefox
```

# TESTING FIREFOX
```
firefox
```
```
apt install hackrf gnuradio rtl-sdr ffmpeg vlc gr-osmosdr
```
```
apt install git unzip
```
```
apt install wget
```
```
cd /home
```
```
wget https://media.githubusercontent.com/media/SitrakaResearchAndPOC/fork_fm_transmitter/main/FM_Transmitter.zip
```
```
unzip FM_Transmitter.zip
```
Commit for the first version : 
```
docker commit bionicmodulation images_bionicmodulation_<arm/intel/amd>:v1.0-fm-transmit
```
```
docker save images_bionicmodulation_<arm/intel/amd>:v1.0-fm-transmit -o images_bionicmodulation_<arm/intel/amd>_v1.0-fm-transmit
```
* Load and run FM transmit
```
docker load -i images_bionicmodulation_<arm/intel/amd>_v1.0-fm-transmit
```
verify images
```
docker images
```
launching processus (container) 
```
docker run -itd --name bionicmodulation-fm --hostname fm --privileged -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro --net=host --env="DISPLAY=$DISPLAY"  --env="LC_ALL=C.UTF-8" --env="LANG=C.UTF-8" images_bionicmodulation_<arm/intel/amd>:v1.0-fm-transmit
```
verify processus (container) 
```
docker ps
```
```
docker exec -it bionicmodulation-fm  hackrf_info
```
Copy the id of the hackr for transmit
```
docker exec -it bionicmodulation-fm  gnuradio-companion
```
Change the id of the hackrf at osmocom_sink  </br>
Change the file to be transmitted </br>
Change at the block QT GUI Frequency bloc, the parameter center_freq, change 106.2e6 to center_freq </br>

# INSTALLING CIPHERING AES AND QUANTUM SAFE AES
```
docker exec -it bionicmodulation bash -c "cd /home; /bin/bash"
```
```
apt update
```
```
apt-get install python3-pip wget
```
```
apt-get install python3-pip
```
```
pip3 install progressbar
```
```
pip3 uninstall numpy
```
POUR ARM SEULEMENT
```
apt install python3-numpy
```
```
pip3 install "numpy<1.20.0"
```
```
apt install python3-distutils
```
#pip3 install click </br>
#https://segmentfault.com/a/1190000040609361 </br>
```
pip3 install "click>7.1.0"
```
```
pip3 show click
```
```
pip3 install progress
```
```
pip3 install sympy
```
```
pip3 install Exit
```
```
apt install -y dh-python python3-click python3-progress  python3-numpy python3-matplotlib python3-networkx   python3-stdeb python3-setuptools-scm python3-setuptools python3-cpuinfo
```
```
pip3 install dh click numpy progress matplotlib networkx stdeb setuptools-scm setuptools
```
Note : 
pip3 install "pillow<5.1.0" </br>
pip3 install "matplotlib<3.1.1"
```
apt-get install python-all
```
## CONSTANT TIME CSIDH AN CRADS
```
git clone https://github.com/Krijn-math/Constant-time-CSURF-CRADS
```
```
cd Constant-time-CSURF-CRADS/
```
```
python3 main.py --help
```
```
python3 main.py -p p512  -m unscaled -s wd2 -v -a csidh -e 5
```
```
python3 main.py -p p512  -m unscaled -s wd1 -v -a csidh -e 10
```
```
python3 main.py -p p512  -m scaled -s wd2 -v -a csidh -e 5
```
```
python3 main.py -p p512  -m unscaled -s wd2 -v -a csurf -e 5
```
FOR MORE EXAMPLE PLEASE SEE [fork Constant-time-CSURF-CRADS](https://github.com/SitrakaResearchAndPOC/fork_Constant-time-CSURF-CRADS) or[original Constant-time-CSURF-CRADS](https://github.com/Krijn-math/Constant-time-CSURF-CRADS)
```
cd ..
```


## INSTALLING
 export PYTHONENCODING=utf_8
update-alternatives --install /usr/bin/python python /usr/bin/python3.8 10
```
git clone https://github.com/JJChiDguez/sibc
```
```
cd sibc
```
Open setup.py by nano
```
nano setup.py
```
search long_description and change :  
```
with open("README.md", "r") as obj : 
```
by
```
with open("README.md", "r", encoding="utf-8") as obj : 
```
```
python3 setup.py bdist_deb
```
```
python3 setup.py install
```
Tape before benchmark csidh
```
export LC_ALL=C.UTF-8
```
```
export LANG=C.UTF-8
```
CASE FOR ARM ONLY
```
pip3 install --upgrade click
```
```
python3 sibc csidh-bench
```
```
python3 sibc -p p512 -f hvelu -a csidh -s df -e 10 csidh-main
```
```
sibc -p p512 -f hvelu -a csidh -s df -e 10 csidh-main
```
## TESTING
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/Cryptodome/main/real_csidh.py
```
```
python3 real_csidh.py 
```

Launching separate mode for csidh sibc
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/Cryptodome/main/keygen_csidh_sibc.py
```
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/Cryptodome/main/shared_csidh_sibc.py
```
```
rm -rf *.pub *.priv *.key
```
```
python3 keygen_csidh_sibc.py -n alice
```
```
ls
```
```
python3 keygen_csidh_sibc.py -n bob
```
```
ls
```
```
python3 shared_csidh_sibc.py -p alice.pub -s bob.priv -k key1.key
```
```
python3 shared_csidh_sibc.py -p bob.pub -s alice.priv -k key2.key
```
The two key should be the same at the two commands
```
cd ..
```

# TESTING AES AND QUANTUM SAFE AES
```
git clone https://github.com/SitrakaResearchAndPOC/Python_PQAES_FO.git
```
```
cd Python_PQAES_FO/
```
```
unzip Python-PQAES.zip 
```
```
cd Python-PQAES-CSIDH/
```
```
python3 AES.py -e test.txt -c 128
```
```
python3 AES.py -d test.txt.aes -c 128
```
Name the decrypted file as :
```
test_dec.txt
```
```
tail -f test_dec.txt
```
```
python3 FO.py 
```
```
python3 FO.py -e test.txt -a sha256 -k bob.priv 
```
```
python3 FO.py -d test.txt.fo -a sha256 -k bob.priv 
```
Named the decipherd document as :
```
test_fo.txt
```
```
tail -f test_fo.txt 
```
```
python3 PQAES.py
```
Commit for the second version : 
```
docker commit bionicmodulation images_bionicmodulation_<arm/intel/amd>:v2.0-crypto
```
```
docker save images_bionicmodulation_<arm/intel/amd>:v2.0-crypto -o images_bionicmodulation_<arm/intel/amd>_v2.0-crypto
```
* Load and run FM transmit
```
docker load -i images_bionicmodulation_<arm/intel/amd>_v2.0-crypto
```
verify images
```
docker images
```
launching processus (container) 
```
docker run -itd --name bionicmodulation-crypto --hostname crypto --privileged -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro --net=host --env="DISPLAY=$DISPLAY"  --env="LC_ALL=C.UTF-8" --env="LANG=C.UTF-8" images_bionicmodulation_<arm/intel/amd>:v2.0-crypto
```
verify processus (container) 
```
docker ps
```


# USE CASE
## ALL TRANSMISSION
* Preparing image
```
xhost +
```
```
docker exec -it bionicmodulation bash -c "cd /home; /bin/bash"
```
```
mkdir all_transmission
```
```
cd all_transmission
```
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/BionicModulationDocker/refs/heads/main/all_transmission/Transmission.zip
```
```
unzip Transmission.zip
```
```
cd transmission
```
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/BionicModulationDocker/refs/heads/main/all_transmission/Test_Taille.zip
```
```
unzip Test_Taille.zip
```
```
wget https://github.com/SitrakaResearchAndPOC/BionicModulationDocker/blob/main/all_transmission/encoded_file.txt
```
```
md5sum encoded_file.txt 
```
cdbea4c82c5f0e20a2b6c46c7ceaddb3  encoded_file.txt
```
rm -rf encoded_file.txt 
```
IN NEW TERMINAL </br>
Find all file and modulation
```
docker exec -it bionicmodulation ls home/all_transmission/transmission/
```
Change the configuration of name file : 
```
docker exec -it bionicmodulation nano home/all_transmission/transmission/encode_file.py 
```
Configure as : </br>
fichier_pdf = 'test.pdf' </br> </br>
Encoding as text for modulation 
```
docker exec -it bionicmodulation bash -c "cd home/all_transmission/transmission/; python3 encode_file.py"
```
Print all file and all modulation
```
docker exec -it bionicmodulation ls home/all_transmission/transmission/encoded_file.txt
```
check md5sum for encoded_file.txt
```
docker exec -it bionicmodulation md5sum home/all_transmission/transmission/encoded_file.txt
```
658a69efae94d3c130cb7cca412677d8  home/all_transmission/transmission/encoded_file.txt </br>
Launch hackrf_info for copying id : </br>
Copy id of hackrf </br>
```
docker exec -it bionicmodulation hackrf_info
```
eg : </br>
0000000000000000355867dc324d7c0b </br>
Launch gnuradio-companion and choose the modulation at /home/all_transmission/transmission
```
docker exec -it bionicmodulation gnuradio-companion
```
Change the path of encoded_file.txt and id of hackrf as copied 

## ALL RECEPTION
```
docker exec -it bionicmodulation bash -c "cd /home; /bin/bash"
```
* Installing pdf viewer for arm
```
apt install mupdf
```
* Installing pdf viewer for ubuntu-desktop
```
apt install xdg-utils
```
Create directory for reception
```
mkdir -p /home/all_reception/
```
```
cd /home/all_reception/
```
Downloads file for reception
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/BionicModulationDocker/refs/heads/main/all_reception/Reception.zip
```
```
unzip Reception.zip
```
IN NEW TERMINAL
Find all files and all modulation at reception
```
docker exec -it bionicmodulation ls home/all_reception/reception/
```
Find id of hackrf to be copyed at the gnuradio-companion
```
docker exec -it bionicmodulation hackrf_info
```
0000000000000000629461dc23815153 </br>
Lauch gnuradio-companion for the demodulation at /home/all_reception/reception </br>
```
docker exec -it bionicmodulation gnuradio-companion
```
Choose the modulation for reception </br>
Change the id of hack_rf </br>
Change the place for osmocom and the name : /home/all_reception/reception/decode_file.txt</br>
Monitor all received file </br>
```
docker exec -it bionicmodulation bash -c "cd home/all_reception/reception/; tail -f decode_file.txt"
```
Launch decoding file </br>
```
docker exec -it bionicmodulation bash -c "cd home/all_reception/reception/; python3 decode_file.py"
```
```
docker exec -it bionicmodulation bash -c "cd home/all_reception/reception/; mupdf decoded_file.pdf"
```
Stop gnuradio-companion and remove the file captured
```
docker exec -it bionicmodulation bash -c "cd home/all_reception/reception/; rm -rf decode_file.txt"
```


# RESUME SAVING IMAGE
```
docker image save bionicmodulation > bionicmodulation.tar.gz
```
# RESUME LAUNCHING 
```
docker run --hostname transmission -tid --privileged -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro --net=host --env="DISPLAY=$DISPLAY"  --env="LC_ALL=C.UTF-8" --env="LANG=C.UTF-8" --name bionicmodulation <image_all>
```

# RESUME LOAD AND RUN
```
docker image load <  bionicmodulation.tar.gz
```
```
xhost +
```
```
docker run -tid --privileged -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro --net=host --env="DISPLAY=$DISPLAY"  --env="LC_ALL=C.UTF-8" --env="LANG=C.UTF-8" --name bionicmodulation bionicmodulation
```
```
docker ps 
```
```
docker exec -ti bionicmodulation hackrf_info
```
```
docker exec -ti bionicmodulation gnuradio-companion
```
