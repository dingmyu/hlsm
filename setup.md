cat /proc/version
lsb_release -a

apt-get --purge remove "*nvidia*"
apt-get auto-remove && apt-get clean && apt-get update && apt-get upgrade
cat /proc/driver/nvidia/version
apt install nvidia-driver-470
reboot
nvidia-smi


wget https://repo.anaconda.com/miniconda/Miniconda3-py38_4.10.3-Linux-x86_64.sh
bash Miniconda3-py38_4.10.3-Linux-x86_64.sh
apt-get install cmake zlib1g-dev

git clone https://github.com/valtsblukis/hlsm.git
cd hlsm/
conda env create -f hlsm-alfred.yml
conda remove -n hlsm-alfred --all
conda env create -f hlsm-alfred.yml
conda activate hlsm-alfred

mkdir workspace
cd workspace/
mkdir alfred_src
cd alfred_src
git clone https://github.com/askforalfred/alfred.git

source init.sh


curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -  # only for docker bugs in installation
sudo chmod a+r /usr/share/keyrings/docker-archive-keyring.gpg  # only for docker bugs in installation

sudo apt update
sudo apt install xrdp xfce4 tightvncserver
echo 'deb http://archive.ubuntu.com/ubuntu/ bionic universe' >> /etc/apt/sources.list
apt-get install -y vnc4server

cd workspace/alfred_src/alfred
sudo python3 ./scripts/startx.py 0

<!-- 
apt-get install -y gvncviewer xtightvncviewer
apt-get install -y x-window-system-core
apt-get install -y gdm3
apt-get install -y ubuntu-desktop
apt-get install -y gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal -->


Install docker following https://docs.docker.com/engine/install/ubuntu/

git clone https://github.com/allenai/ai2thor-docker
cd ai2thor-docker
./scripts/build.sh
editing ai2thor-docker/scripts/run.sh with --privileged
./scripts/run.sh
