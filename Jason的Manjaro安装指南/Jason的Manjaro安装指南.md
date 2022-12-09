# Jason的Manjaro安装指南

## 0x01 安装系统（Win11+ManjaroKDE）

- Rufus制作U盘启动盘

- BIOS设置
  - 关闭快速启动（Fast Boot）
  - 关闭安全启动（Secure Boot）
    - 高级 -> 安全启动 -> 编辑 -> 删除所有密钥 -> 安全启动自动关闭（Disable）
- 磁盘分区
  - 512MB Boot分区
    - 文件类型：FAT32
    - 挂载点：/boot/efi
    - 其他：勾选boot选项
  - 40GB Root分区
    - 文件类型：ext4
    - 挂载点：/
    - 其他：勾选root选项
  - 100GB Home分区
    - 文件类型：ext4
    - 挂载点：/home
    - 其他：勾选home选项
  - **<font color="red">存疑</font>**8GB Swap分区
    - 文件类型：swap
    - 挂载点：swap
    - 其他：勾选swap
- Windows的分区可以不管他，理论上这样就能够实现双启动

## 0x02 系统配置

### [pacman包管理器使用详细介绍（官网）](https://wiki.archlinuxcn.org/wiki/Pacman)

### 常用命令

- **强制更新系统库**并**更新所有软件**

  ```bash
  $ sudo pacman -Syyu
  ```

- 安装 

  ```bash	
  $ sudo pacman -S [PKG]
  ```

- 卸载

  ```bash
  $ sudo pacman -R [PKG]
  ```

- 未完待续……

### 更换国内源 & 更新系统

```bash
$ sudo pacman-mirrors -c China
$ sudo pacmna -Syyu
```

### 安装必要软件

```bash
$ sudo pacman -S neovim vscode ...
```

- neovim
- vscode
- yay：[详情介绍](https://zhuanlan.zhihu.com/p/363666022 "知乎专栏")
- base-devel：（或许是develop？）一些常用的开发工具
- jdk11-openjdk
- debtap：安装deb包文件工具 [简单使用教程](#安装deb包文件)
- tree：树状目录表
- netease-cloud-music：网易云音乐（竟然可以直装！）
- [scrcpy](https://github.com/Genymobile/scrcpy)：ADB连接手机获取图像并控制，通常配合[sndcpy](https://github.com/rom1v/sndcpy)使用，后者为传输声音
- typora：Markdown编辑/阅读器*（付费/可试用）*
- uget：多线程下载器（可下载磁链）

### 拼音输入法安装

使用`IBus`和`Rime`

```bash
$ sudo pacman -S ibus ibus-rime
```

**<font color="red">存疑</font>**（以下代码存疑：KDE桌面环境下是否会执行 ~/.xprofile？不过可以正常使用）

```bash
$ touch ~/.xprofile
```

输入以下内容

```bash
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
ibus-daemon -x -d
```

重启即可使用

[Rime（中州韵）配置](#Rime输入法引擎配置)

## 0x03 其他

### 安装deb包文件

第一次执行前先更新

```bash
$ sudo debtap -u
```

转换为pacman可安装的格式

```bash
$ debtap *.deb
```

会生成`*.pkg.tar.zst`的文件

```bash
$ sudo pacman -U *.pkg.tar.zst
```

安装完成

### Rime输入法引擎配置

在Rime的用户目录下新建`ibus_rime.custom.yaml`和`default.custom.yaml`（默认在`~/.config/ibus/rime/`下）

**<font color="red">存疑</font>**两个文件有不同功用（但还没搞清），写入如下

**ibus_rime.custom.yaml**

```yaml
patch:
    "style/horizontal": true
```

将候选词变为水平排布（默认为竖直排布）

**default.custom.yaml**

```yaml
patch:
    schema_list:
        - schema: luna_pinyin_simp
```

将默认输入法方案：明月拼音_简体字（默认为繁体）

### Github访问加速

工具：[`Fastgithub`](https://github.com/dotnetcore/FastGithub)

未完待续……

[https://github.com/rom1v/sndcpy]: 