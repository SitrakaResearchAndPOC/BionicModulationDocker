```
apt install -y gnuradio gr-osmosdr uhd-host libuhd-dev \
cmake g++ libboost-all-dev libgmp-dev swig python-numpy python-mako \
python-sphinx python-lxml doxygen libfftw3-dev libcomedi-dev libcppunit-dev \
libgsl-dev libusb-1.0-0-dev python-gi python-click python-click-plugins \
python-zmq python-scipy python-matplotlib git
```

```
sudo apt install -y gnuradio gr-osmosdr uhd-host libuhd-dev \
libvolk1-bin libvolk1-dev \
cmake g++ libboost-all-dev libgmp-dev swig python-numpy python-mako \
python-sphinx python-lxml doxygen libfftw3-dev libcomedi-dev libcppunit-dev \
libgsl-dev libusb-1.0-0-dev python-gi python-click python-click-plugins \
python-zmq python-scipy python-matplotlib git
```
```
git clone https://github.com/kit-cel/gr-fbmc.git
```
```
cd gr-fbmc
```
```
mkdir build
```
```
cd build
```
```
cmake ..
```
```
make -j$(nproc)
```
```
make install
```
```
ldconfig
```
```
gnuradio-companion
```
```
python -c "import fbmc; print(fbmc)"
```
