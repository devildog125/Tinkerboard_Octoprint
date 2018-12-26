#!/bin/bash

cd ~
sudo apt update
sudo apt install python-pip python-dev python-setuptools python-virtualenv git libyaml-dev build-essential
mkdir OctoPrint && cd OctoPrint
sudo /usr/bin/easy_install virtualenv
virtualenv venv
source venv/bin/activate
pip install pip --upgrade
pip install https://get.octoprint.org/latest

deactivate

sudo usermod -a -G tty linaro
sudo usermod -a -G dialout linaro

wget https://github.com/foosel/OctoPrint/raw/master/scripts/octoprint.init && sudo mv octoprint.init /etc/init.d/octoprint
wget https://github.com/foosel/OctoPrint/raw/master/scripts/octoprint.default && sudo mv octoprint.default /etc/default/octoprint
sudo chmod +x /etc/init.d/octoprint

sudo service octoprint stop
sudo apt-get install haproxy

wget https://github.com/devildog125/Tinkerboard_Octoprint/blob/master/haproxy.cfg && sudo mv haproxy.cfg /etc/haproxy/haproxy.cfg

sudo pip install numpy