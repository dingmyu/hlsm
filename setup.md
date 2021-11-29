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


# Romote Desktop
sudo apt update
sudo apt install xrdp xfce4  # tightvncserver
echo 'deb http://archive.ubuntu.com/ubuntu/ bionic universe' >> /etc/apt/sources.list
apt-get install -y vnc4server

sudo apt-get install xfce4-terminal  # use xfce4-terminal for better terminal experience, support copy and paste

## If we use xrdp
echo xfce4-session > ~/.xsession

login on port ip:3389 with username

you will have a display named rdp0, you can get the display alias by `echo $DISPLAY`


## If we use xvnc
vncserver :1

vim ~/.vnc/xstartup
```
#!/bin/sh 
unset SESSION_MANAGER 
unset DBUS_SESSION_BUS_ADDRESS 
startxfce4 & 
 
[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
```

vncserver -kill :1
vncserver :1

login on ip (or 3389 + random passwd) and then choose vnc-any, 127.0.0.1, port 5901 with vnc passwd

you can also install gnome and vim ~/.vnc/xstartup
```
apt-get install -y gvncviewer xtightvncviewer
apt-get install -y x-window-system-core
apt-get install -y gdm3
apt-get install -y ubuntu-desktop
apt-get install -y gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
```

```
#!/bin/sh

unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

export XKL_XMODMAP_DISABLE=1
export XDG_CURRENT_DESKTOP="GNOME-Flashback:GNOME"
export XDG_MENU_PREFIX="gnome-flashback-"


[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &

gnome-session --builtin --session=gnome-flashback-metacity --disable-acceleration-check --debug &
nautilus &
gnome-terminal &              
```


cd workspace/alfred_src/alfred
sudo python3 ./scripts/startx.py 0
export DISPLAY=:0

If pytorch is not work (3090):
pip install torch===1.7.1+cu110 torchvision===0.8.2+cu110 torchaudio===0.7.2 -f https://download.pytorch.org/whl/torch_stable.html
<!-- conda install -c anaconda cudatoolkit
conda install pytorch torchvision torchaudio cudatoolkit=11.2 -c pytorch
conda install -c pytorch torchvision cudatoolkit=10.1 pytorch  -->

pip install jupyterlab
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb
/usr/bin/google-chrome

jupyter lab --ip 0.0.0.0 --no-browser

# Docker
Install docker following https://docs.docker.com/engine/install/ubuntu/

git clone https://github.com/allenai/ai2thor-docker
cd ai2thor-docker
./scripts/build.sh
editing ai2thor-docker/scripts/run.sh with --privileged, and removing the example.py
./scripts/run.sh

sudo apt-get install xorg openbox  # in docker
python3 scripts/startx.py 0


# BUGs
1. Sorry, command-not-found has crashed!
> sudo chmod o+r /var/lib/command-not-found/commands.db
