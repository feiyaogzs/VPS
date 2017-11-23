# VPS
Virtual private server related

Setup Simple PPTP VPN server for CentOS and Ubuntu
==================================================

> NOTE: PPTP VPN is considered insecure. Do not rely for this vpn
> if you need security. However, PPTP works out of the box on many
> operating systems, including many Linux distributions, Windows, 
> Mac OS and Android and it's easily good enough for evading country
> level IP blocks.

CentOS-pptp-setup.sh has been tested on **Vultr & Host1plus: CentOS 6 x86**

Ubuntu-pptp-setup.sh has been tested on **Vultr & Host1plus: Ubuntu14.04 x86**

CentOS7-pptp-host1plus.sh is just for **CentOS 7** on **Host1plus & OpenVZ**

INSTALLATION INSTRUCTIONS
=========================

**CentOS**
------

    wget https://raw.githubusercontent.com/DanylZhang/VPS/master/CentOS-pptp-setup.sh
    chmod +x ./CentOS-pptp-setup.sh
    ./CentOS-pptp-setup.sh -u your_username -p your_password

**Ubuntu**
------

    wget https://raw.githubusercontent.com/DanylZhang/VPS/master/Ubuntu-pptp-setup.sh
    sudo bash Ubuntu-pptp-setup.sh -u your_username -p your_password
    service pptpd restart

*or*

**CentOS 7**
------

    wget https://raw.githubusercontent.com/DanylZhang/VPS/master/CentOS7-pptp-host1plus.sh
    chmod +x ./CentOS7-pptp-host1plus.sh
    ./CentOS7-pptp-host1plus.sh -u your_username -p your_password

Some notes
==========
If your vpn password **less than 8** characters,then give you a random password.

To add more accounts, see the file /etc/ppp/chap-secrets

If you keep the vpn server generated with this script on the internet for a
long time (days or more), consider either restricting access to the ssh port on
the server by ip addresses to the networks you use, if you know the addresses
you are most likely to use or at least change ssh from port 22 to a random
port.

You can also specify you own username and password, run `./CentOS-pptp-setup.sh -h`
*or* `sudo bash Ubuntu-pptp-setup.sh -h` for help.



Centos7搭建pptp一键安装脚本

废话不多说，先上脚本地址：Centos7一键pptp

使用：

wget https://raw.githubusercontent.com/DanylZhang/VPS/master/CentOS7-pptp-host1plus.sh
chmod +x ./CentOS7-pptp-host1plus.sh
./CentOS7-pptp-host1plus.sh -u your_username -p your_password
1
2
3
可在-u、-p后随意更改自己的登录用户名和密码。但密码长度必须大于8个 ASCII字符，否则为了安全，脚本将会随机生成密码。



注：

如果你无法访问一些特定网站，建议你修改ppp接口的MTU（很多时候能连接vpn但是无法打开某些网页也可能跟这个有关系）

输入vi /etc/ppp/ip-up

在倒数第二行加入如下内容：/sbin/ifconfig $1 mtu 1400

缺省 MTU:1496

保存后需要重启PPTP服务器，指令如下: systemctl restart pptpd

也可以不更改ip-up文件，而是在/etc/ppp/下新建ip-up.local文件。指令如下：

cat > /etc/ppp/ip-up.local << END
/sbin/ifconfig $1 mtu 1400
END
chmod +x /etc/ppp/ip-up.local
1
2
3
4
该脚本使用的是后者。

附上其他linux发行版的pptp vpn一键安装脚本的Github地址：pptp一键脚本
