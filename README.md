# PupperGuide

### 烧录树莓派操作系统

下载烧录软件 Raspberry Pi Imager  https://www.raspberrypi.org/software/

苹果电脑 https://downloads.raspberrypi.org/imager/imager_latest.dmg

Windows https://downloads.raspberrypi.org/imager/imager_latest.exe

Ubuntu（x86） https://downloads.raspberrypi.org/imager/imager_latest_amd64.deb

选择 Raspberry Pi OS

## 设置SSH https://www.raspberrypi.org/documentation/remote-access/ssh/README.md

在树莓派SD卡的根目录里放置一个名为ssh的文件，不要文件扩展名，文件无需任何内容

## 查看树莓派局域网IP地址

### 方法一：用电脑登录网关查

http://192.168.1.1

（例如查到有线连接设备IP: 192.168.1.26）

### 方法二：局域网内电脑终端命令查看

https://www.raspberrypi.org/documentation/remote-access/ip-address.md

ping raspberrypi.local

PING raspberrypi.local (192.168.1.26): 56 data bytes

64 bytes from 192.168.1.26: icmp_seq=0 ttl=64 time=3.608 ms

64 bytes from 192.168.1.26: icmp_seq=1 ttl=64 time=2.008 ms

64 bytes from 192.168.1.26: icmp_seq=2 ttl=64 time=3.669 ms

64 bytes from 192.168.1.26: icmp_seq=3 ttl=64 time=5.249 ms

### 在电脑终端登录树莓派

ssh pi@192.168.1.26

pi@192.168.1.26's password: raspberry

### 更新软件包列表

sudo apt-get update


### 安装python pip/pip3

https://packaging.python.org/guides/installing-using-linux-tools/#installing-pip-setuptools-wheel-with-linux-package-managers

## Python 2:

sudo apt install python-pip

## Python 3:
（sudo apt install python3-venv python3-pip）

sudo apt install python3-pip

## 安装git:

sudo apt install git

## 安装 pigpio (pigpiod)
wget https://github.com/joan2937/pigpio/archive/refs/tags/v79.zip

unzip v79.zip

cd pigpio-79

make

sudo make install

cd ..

## 安装robot (需要在pi用户目录下 cd ~)

```
cd ~

# UDPComms
git clone https://github.com/qdpupper/UDPComms.git
cd UDPComms
sudo bash install.sh
cd ..


# PS4Joystick
#git clone https://github.com/stanfordroboticsclub/PS4Joystick.git
git clone https://github.com/qdpupper/PS4Joystick.git
cd PS4Joystick
sudo bash install.sh
cd ..


# joystick.service

#git clone https://github.com/stanfordroboticsclub/PupperCommand.git
git clone https://github.com/qdpupper/PupperCommand.git
cd PupperCommand
sudo bash install.sh
cd ..

#StanfordQuadruped
git clone https://github.com/qdpupper/StanfordQuadruped.git
cd StanfordQuadruped
sudo bash install.sh
cd ..
```

## 查看服务运行状态

sudo systemctl status robot

sudo systemctl status joystick

### 完成

### 由于github网络连接不稳定，没有安装成功的可以手动安装
////ln: failed to create symbolic link '/lib/systemd/system/joystick.service': File exists

pi@raspberrypi:~/pupper/StanfordQuadruped $ sudo ln -s $(realpath .)/robot.service /etc/systemd/system/

ln: failed to create symbolic link '/etc/systemd/system/robot.service': File exists

pi@raspberrypi:~/pupper/StanfordQuadruped $ sudo ln -sf $(realpath .)/robot.service /etc/systemd/system/


#changes by Juedongli
https://github.com/qdpupper/UDPComms/blob/master/UDPComms.py

```

    def send(self, obj):
        """ Publish a message. The obj can be any nesting of standard python types """
        msg = msgpack.dumps(obj, use_bin_type=False)
        assert len(msg) < MAX_SIZE, "Encoded message too big!"
        
        #self.sock.send(msg)
        #changed by Juedongli
        try:
            self.sock.send(msg)
        except:
            print("error: self.sock.send(msg) ConnectionRefusedError")
            
```


