1. **pbuilder + qemu**

以下操作基于debian11环境,其他环境下需注意qemu版本是否在5.2版本以上

```plain
sudo apt install pbuilder qemu qemu-user-static pigz
```

配置 /etc/pbuilderrc

```plain
MIRRORSITE=https://mirrors.aliyun.com/debian-ports/
DEBOOTSTRAPOPTS=(
    '--variant=buildd'
    '--no-check-gpg'
    )
COMPRESSPROG="pigz"
DEBOOTSTRAP=qemu-debootstrap
PBUILDERSATISFYDEPENDSCMD="/usr/lib/pbuilder/pbuilder-satisfydepends-apt"
```

创建base环境

```plain
sudo dpkg --add-architecture riscv64 
sudo pbuilder create --debootstrapopts --arch --debootstrapopts riscv64 --mirror "https://mirrors.aliyun.com/debian-ports/" --distribution sid --basetgz buster-riscv64.tgz 
```



