# Archlinux-install

### 分区

* `cfdisk`

  * /dev/sda1   /boot

  * /dev/sda2   /

  * /dev/sda3   /home

  * /dev/sda4   swap

### 格式化分区

* `mkfs.ext4 /dev/sda1`

* `mkfs.ext4 /dev/sda2`

* `mkfs.ext4 /dev/sda3`

* `mkswap /dev/sda4`

* `swapon /dev/sda4`

### 挂载分区

* `mount /dev/sda2 /mnt`

* `mkdir /mnt/{boot,home}`

* `mount /dev/sda1 /mnt/boot`

* `mount /dev/sda3 /mnt/home`


### 选择更新源

* `nano /etc/pacman.d/mirrorlist`

 ```bash
  Server = http://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
  Server = http://mirror.bjtu.edu.cn/archlinux/$repo/os/$arch
 ```

### 启用网络

* `dhcpcd`

### 安装基本系统

* `pacstrap -i /mnt base base-devel net-tools`

### 生成fstab

* `genfstab -U -p /mnt >> /mnt/etc/fstab`

### 基本系统设置

* `arch-chroot /mnt /bin/bash`    #进入基本系统

* `nano /etc/locale.gen`    #设置语言，至少开启en_US.UTF-8和zh_CN.UTF-8

* `locale-gen`    #刷新locale

* `echo LANG=en_US.UTF-8 >> /etc/locale.conf`    #设置默认语言

* `nano /etc/vconsole.conf`    #设置console

 ```bash
 KEYMAP=us
 FONT=
 ```

### 设置时间

* `ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`
* `hwclock --systohc --utc`    #硬件时间

### 设置主机名

* `echo kai-arch > /etc/hostname`
* `nano /etc/hosts`    #修改hosts添加hostname

### 创建 ramdisk 环境

* `mkinitcpio -p linux`

### 用戶設置

* `passwd`    #为root设置密码

* `useradd -m -g users -G wheel -s /bin/bash simpkae`    #创建普通用户

* `passwd simpkae`    #设置密码

* `EDITOR=nano visudo`    #配置权限，去掉%wheel ALL=(ALL) ALL的注释

### 安装图形界面

* `pacman -S xf86-video-vmware`    #安装显卡驱动

* `pacman -S xf86-input-evdev`    #安装键鼠驱动

* `pacman -S open-vm-tools`    #安裝vmtools工具

* `systemctl enable vmware-vmblock-fuse.service`    #开机启动vmtools

* `pacman -S xorg-server xorg-server-utils xorg-xinit`    #安装X环境

* `pacman -S ttf-dejavu wqy-zenhei wqy-microhei`    #安装字体

* `pacman -S mate mate-extra`    #安装mate

* `pacman -S xfce4`    #安装xfce4

* `pacman -S lxdm`    #安装启动器

* `systemctl enable lxdm`    #自动启动

### 配置网络

* `pacman -S networkmanager`

* `pacman -S network-manager-applet xfce4-notifyd`

* `systemctl enable NetworkManager`

### 安装引导

* `pacman -S grub-bios`

* `grub-install /dev/sda`

* `grub-mkconfig -o /boot/grub/grub.cfg`

### 重启

* `exit`

* `umount -R /mnt/{boot,home}`

* `umount -R /mnt`

* `reboot`

### 设置终端颜色

* `nano ~/.bashrc`

 ```bash
 #PS1='[\u@\h \W]\$ '  # Default
 PS1="\[\033[40;33;1m\][\!]\`if [[ \$? =   "0" ]]; then echo "\\[\\033[32m\\]"; else echo   "\\[\\033[31m\\]"; fi\`[\u@\h: \`if [[ `pwd|wc -c|tr -d "   "` > 18 ]]; then echo "\\W"; else echo "\\w";   fi\`]\\$\[\033[0m\] "; echo -ne "\033]0;`hostname -s`:`pwd`\007"
 ```

### 安裝fcitx软件

* `sudo pacman -S fcitx-im`    #安装fcitx输入法

* `nano ~/.xinitrc`

 ```bash
 export LANG=zh_CN.UTF-8
 export LC_ALL="zh_CN.UTF-8"
 export GTK_IM_MODULE=fcitx
 export QT_IM_MODULE=fcitx
 export XMODIFIERS="@im=fcitx"
 ```

### 安裝firefox浏览器

* `sudo pacman -S firefox firefox-i18n-zh-cn`

### 安裝Gvim

* `sudo pacman -S gvim-python3`

### 时间同步

* `sudo timedatectl set-ntp true`
