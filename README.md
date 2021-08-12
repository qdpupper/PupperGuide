# PupperGuide

烧录树莓派操作系统

设置SSH https://www.raspberrypi.org/documentation/remote-access/ssh/README.md

在树莓派SD卡的分区里放置一个名为ssh的文件，没有文件扩展名，文件无需任何内容

查看树莓派局域网IP地址 方法一：用电脑登录网关查

http://192.168.1.1

（例如查到有线连接设备IP: 192.168.1.26）

方法二：局域网内电脑终端命令查看

https://www.raspberrypi.org/documentation/remote-access/ip-address.md

ping raspberrypi.local

PING raspberrypi.local (192.168.1.26): 56 data bytes

64 bytes from 192.168.1.26: icmp_seq=0 ttl=64 time=3.608 ms

64 bytes from 192.168.1.26: icmp_seq=1 ttl=64 time=2.008 ms

64 bytes from 192.168.1.26: icmp_seq=2 ttl=64 time=3.669 ms

64 bytes from 192.168.1.26: icmp_seq=3 ttl=64 time=5.249 ms

在电脑终端登录树莓派

ssh pi@

ssh pi@192.168.1.26

pi@192.168.1.26's password: raspberry


sudo apt-get update


安装python pip/pip3

https://packaging.python.org/guides/installing-using-linux-tools/#installing-pip-setuptools-wheel-with-linux-package-managers

Python 2:

sudo apt install python-pip

Python 3:

#sudo apt install python3-venv python3-pip
sudo apt install python3-pip

git:

sudo apt install git

安装

git clone https://github.com/qdpupper/StanfordQuadruped.git

cd StanfordQuadruped sudo bash install.sh

////

pi@raspberrypi:~/pupper/StanfordQuadruped $ sudo ln -s $(realpath .)/robot.service /etc/systemd/system/ ln: failed to create symbolic link '/etc/systemd/system/robot.service': File exists

pi@raspberrypi:~/pupper/StanfordQuadruped $ sudo ln -sf $(realpath .)/robot.service /etc/systemd/system/





