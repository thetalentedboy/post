
# 写在前面
本文为个人使用的一些好用工具推荐及配置教程，可以视为备忘录，发行版为arch linux。

# 桌面环境
linux下主流桌面环境主要分为两派，实用党和极客党。
- 实用党主张使用`DE(desktop environment)`，即完整的桌面环境，功能和相关基础设施都是比较完整，WM是他的组成部分。如：KDE，gnome...
- 极客党主张使用`WM(windows manage)`，WM只包含了窗口管理的逻辑，大部分操作都在终端内完成，它可以完全定制自己的一切功能，对系统自定义要求比较高的可以使用。我之前也是很喜欢用WM的，但缺点是缺少很多基础的工具，而且很容易出问题，几乎任何拓展功能都需要自己手动去安装和折腾，不适合不喜欢折腾的人。如： dwm，Hyprland，i3wm...
#### KDE
我现在使用kde作为日常使用，使用wm多少会有一些不太方便，而且会时不时出一些bug，,使用完善的de可以避免很多问题，kde就是一个很好的选择。

#### dwm
`dwm`是由suckless社区，一群追求极简的程序员来开发的wm环境，不同与普遍意义上的桌面环境DE，他只有窗口管理，源码只有三千行，自由度非常高，依赖`x11`。

#### Hyprland
`Hyprland`是`wayland`环境下最活跃的WM项目，它的默认风格很极客，做了一定的封装，在自由度上不如`dwm`。
<br>
`wayland`是一个`x11`的竞品，它想一统linux图形显示协议，但是它有很多bug不太稳定，这个也是我放弃它的原因之一。

# 虚拟机
当有一些需要使用window的场景，比如调试外设配置，使用指纹软件之类的需求时，window是唯一选择。
下面是我使用的虚拟机方案。
<br>
`libvirt + KVM/QEMU`，我选用的客户端软件是Virt-manager，具体配置详见 https://wiki.archlinuxcn.org/wiki/Libvirt

# 软件集合
以下是软件备忘录，为arch pkg或aur包名，重装系统时方便一键安装。

```
yay
linuxqq
wechat-universal-bwrap
dingtalk-bin
netease-cloud-music
docker
docker-compose
kubectl
postman-bin
fcitx5-im
fcitx5-chinese-addons
google-chrome
okular-git
visual-studio-code-bin
nvim
neovim-git
keyd-git
spectacle
font-manager
libvirt
Virt-manager
```
 
