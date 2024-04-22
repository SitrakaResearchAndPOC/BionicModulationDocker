# BionicModulationDocker
# INSTALLATION OF MODULATION
## preparing image
```
xhost +
```
```
docker image pull ubuntu:18.04
```
```
docker run -tid --privileged -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro --net=host --env="DISPLAY=$DISPLAY"  --name bionicmodulation ubuntu:18.04
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

## testing firexfox
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
mkdir FM-Modulation
```
```
cd FM-Modulation
```
```
wget https://media.githubusercontent.com/media/SitrakaResearchAndPOC/fork_fm_transmitter/main/FM_Transmitter.zip
```
```
unzip FM_Transmitter.zip
```
## open new terminal :
```
docker ps
```
get the id : 
```
docker commit <id> bionicmodulation
```
verify
```
docker images 
```
PLUG HACKRF AND VERIFY
```
hackrf_info
```
# INSTALLING CIPHERING AES AND QUANTUM SAFE AES
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
## constant time csurf and crads
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


## installing sibc
 export PYTHONENCODING=utf_8
```
update-alternatives --install /usr/bin/python python /usr/bin/python3.8 10
```
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
```
python3 sibc csidh-bench
```
```
python3 sibc -p p512 -f hvelu -a csidh -s df -e 10 csidh-main
```
```
sibc -p p512 -f hvelu -a csidh -s df -e 10 csidh-main
```
## Testing : 
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
```
Name the decrypted file as test_dec.txt
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
```
tail f test_fo.txt 
```
```
python3 PQAES.py
```

# SAVING IMAGE
```
docker image save bionicmodulation > bionicmodulation.tar.gz
```

# LOAD AND RUN
```
docker image load <  bionicmodulation.tar.gz
```
```
xhost +
```
```
docker run -tid --privileged -v /dev/bus/usb:/dev/bus/usb -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro --net=host --env="DISPLAY=$DISPLAY" --name bionicmodulation bionicmodulation
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
