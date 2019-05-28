# RL-PX4 Project
**work in progress**
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
Host pi   # this name `pi` is importent
  Hostname     <IP>
  User         <USER>
  Port         <PORT>
  IdentityFile <SSH_KEY_FILE>
```


3. Download (may take a while)
```bash
git clone <RLQuadrotorProject.git>
cd RLQuadrotorProject
git checkout docking_NavioPi_Simulator
git submodule init
git submodule update
```


4. Compile


**UPLOAD NEURAL NETWORK**
In
```bash
<RLQuadrotorProject>/NavioPi/Firmware/src/modules/hrl_control/CMakeLists.txt
```
Edit:
```bash
execute_process(COMMAND
                    make
                WORKING_DIRECTORY
                    <RLQuadrotorProject>/NavioPi/Firmware/src/modules/hrl_control/neural_network)
```
This will upload the neural network at first execute cmake

or you can just run
```bash
cd <RLQuadrotorProject>/NavioPi/Firmware/src/modules/hrl_control/neural_network
make
```


Compile
```bash
python3 -m venv QUAD_RL
echo "export PATH=\${PATH}:${PWD}/NavioPi/rpi-tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin" >> QUAD_RL/bin/activate
source QUAD_RL/bin/activate
pip3 install -r requirements.txt
cd NavioPi/Firmware
make emlid_navio2_rl_cross upload
```


5. Running
```bash
ssh pi
sudo emlid_navio2_rl_cross/bin/px4 -s hrl_control.config
```

## Running remote_monitor
**work in progress**
1. Run hrl_control
```bash
ssh pi
sudo emlid_navio2_rl_cross/bin/px4 -s hrl_control.config
pxh> hrl_control register_partner <id> <ip> <port> #e.g. 0 192.168.1.255 8889  
```
  -  -note-
      1. \<id\> is not importent so far
      2. \<ip\> is the ip of computer which running monitor
      3. \<port\> is port

2. Run monitor
```bash
cd <RLQuadrotorProject>
source QUAD_RL/bin/activate
pip3 install -I ./Simulator
cd Simulator/quad/remote_monitor
python3 monitor.py
```

