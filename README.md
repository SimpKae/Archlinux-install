# Archlinux-install

### 分区

* #### `cfdisk`

  * /dev/sda1   /boot

  * /dev/sda2   /

  * /dev/sda3   /home

  * /dev/sda4   swap
  
### 格式化分区

* #### `mkfs.ext4 /dev/sda1`

* #### `mkfs.ext4 /dev/sda2`

* #### `mkfs.ext4 /dev/sda3`

* #### `mkswap /dev/sda4`

* #### `swapon /dev/sda4`

### 挂载分区

* #### `mount /dev/sda2 /mnt`

* #### `mkdir /mnt/{boot,home}`

* #### `mount /dev/sda1 /mnt/boot`

* #### `mount /dev/sda3 /mnt/home`

### 选择更新源

* #### `nano /etc/pacman.d/mirrorlist`

  * Server = http://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
  
  * Server = http://mirror.bjtu.edu.cn/archlinux/$repo/os/$arch
  
### 启用网络

* #### `dhcpcd`

### 安装基本系统

* #### `pacstrap -i /mnt base base-devel net-tools`


  
