# RL-PX4 Project

## Minimum install
1. Dependence
```bash
sudo apt update 
sudo apt install git zip cmake build-essential genromfs ninja-build exiftool astyle -y
sudo apt install xxd -y
```

2. Setup ssh config
e.g.
```hash
Host pi
  Hostname     <IP>
  User         <USER>
  Port         <PORT>
  IdentityFile <SSH_KEY_FILE>
```


3. Download (may take a while)
```bash
git clone <RLQuadrotorProject.git>
cd RLQuadrotorProject
git submodule init
git submodule update
```
may take a while.


4. Compile
```bash
python3 -m venv QUAD_RL
echo "export PATH=\${PATH}:${PWD}/NavioPi/rpi-tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin" >> QUAD_RL/bin/activate
source QUAD_RL/bin/activate
pip3 install -r requirements.txt
cd NavioPi/Firmware
make emlid_navio2_cross upload
```
