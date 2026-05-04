```markdown
This variant of adbfs works even WITHOUT having root access (busybox) on your phone!

## Windows

You will need [WinFsp](https://winfsp.dev/) and `adb`.

Download the latest `adbfs.exe` from [Releases](../../releases).

Create a mount point if needed (e.g. in your home directory):

    mkdir C:\droid

You can now mount your device:

    adbfs C:\droid

Have fun!

## Ubuntu

You will need `libfuse-dev` and `adb`. You will also need `build-essential`, `git`, and `pkg-config`.

    sudo apt-get install libfuse-dev android-tools-adb
    sudo apt-get install build-essential git pkg-config

Clone the repository:

    git clone git@github.com:spion/adbfs-rootless.git
    cd adbfs-rootless

Build:

    make

Optional: If you have a separate copy of android-sdk and would
like to use that adb, copy the binary adbfs to the `android-sdk/platform-tools`
directory. If platform-tools is in your $PATH you can skip this step.

Create a mount point if needed (e.g. in your home directory):

    mkdir ~/droid

You can now mount your device (also from the platform-tools dir):

    ./adbfs ~/droid

If you want to trigger a media rescan after every operation, use the option `-o rescan`:

    ./adbfs -o rescan ~/droid

Have fun!

## MacOS

Install adb and fuse

    brew install --cask android-platform-tools
    brew install --cask macfuse

Check access to phone through adb

    adb devices

Clone the repository:

    git clone https://github.com/spion/adbfs-rootless.git
    cd adbfs-rootless

Build:

    make

Create a mount point if needed (e.g. in your home directory):

    mkdir ~/droid

Mount your device (You will be asked and have to allow fuse extension):

    ./adbfs ~/droid

Have fun!

## Troubleshooting

### Error: device not found

When running you get the following error:

```
--*-- exec_command: adb shell ls
error: device not found
```

Solution: Make sure that [USB Debugging is enabled][enable-usb-debug].

Then `fusermount -u /media/mount/path` before trying again. Note that if for any reason `fusermount` is not available in your system, you can use `sudo umount /media/mount/path` instead.

### Error: device offline

When running you get the following error:

```
--*-- exec_command: adb shell ls
error: device offline
```

Solution: Make sure that

1. Your android-sdk-tools are up to date. Newer versions
   of Android also require newer versions of adb. For more info, see 
   [this Stack Overflow post][error-device-offline].

2. You answer `Yes` when your phone asks whether it should allow the 
   computer with the specified RSA key to access the device.

Then `killall -9 adb; fusermount -u /media/mount/path` before trying again.

[enable-usb-debug]: http://www.droidviews.com/how-to-enable-developer-optionsusb-debugging-mode-on-devices-with-android-4-2-jelly-bean/
[error-device-offline]: http://stackoverflow.com/questions/10680417/error-device-offline
```
---------------------------------------------------------------------------

```markdown
## 中文说明

本项目是 [adbfs-rootless](https://github.com/spion/adbfs-rootless) 的 Windows 分支，原作者为 **spion**，保留所有原始内容和署名。

本分支提供预编译的 Windows 可执行文件，无需从源码编译。

### Windows

你需要安装 [WinFsp](https://winfsp.dev/) 和 `adb`。

从 [Releases](../../releases) 页面下载最新的 `adbfs.exe`。

如果需要，创建一个挂载点（例如在你的用户目录下）：

    mkdir C:\droid

现在你可以挂载你的设备了：

    adbfs C:\droid

祝你用得开心！

### Ubuntu

你需要安装 `libfuse-dev` 和 `adb`，以及 `build-essential`、`git` 和 `pkg-config`。

    sudo apt-get install libfuse-dev android-tools-adb
    sudo apt-get install build-essential git pkg-config

克隆仓库：

    git clone git@github.com:spion/adbfs-rootless.git
    cd adbfs-rootless

构建：

    make

可选：如果你有单独的 android-sdk 并且想使用其中的 adb，将 adbfs 二进制文件复制到 `android-sdk/platform-tools` 目录中。如果 platform-tools 已经在你的 $PATH 中，可以跳过此步骤。

如果需要，创建一个挂载点（例如在你的 home 目录下）：

    mkdir ~/droid

现在你可以挂载你的设备了（也可以从 platform-tools 目录执行）：

    ./adbfs ~/droid

如果想在每次操作后触发媒体重新扫描，使用 `-o rescan` 选项：

    ./adbfs -o rescan ~/droid

祝你用得开心！

### MacOS

安装 adb 和 fuse：

    brew install --cask android-platform-tools
    brew install --cask macfuse

通过 adb 检查手机连接：

    adb devices

克隆仓库：

    git clone https://github.com/spion/adbfs-rootless.git
    cd adbfs-rootless

构建：

    make

如果需要，创建一个挂载点（例如在你的 home 目录下）：

    mkdir ~/droid

挂载你的设备（系统会询问并需要你允许 fuse 扩展）：

    ./adbfs ~/droid

祝你用得开心！

### 故障排除

#### 错误：找不到设备

当你运行时出现以下错误：

```
--*-- exec_command: adb shell ls
error: device not found
```

解决方案：确保已开启 [USB 调试][enable-usb-debug]。

重试之前先执行 `fusermount -u /media/mount/path`。注意，如果系统中没有 `fusermount`，可以使用 `sudo umount /media/mount/path` 代替。

#### 错误：设备离线

当你运行时出现以下错误：

```
--*-- exec_command: adb shell ls
error: device offline
```

解决方案：确保以下两点

1. 你的 android-sdk-tools 是最新的。新版本的 Android 也需要更新版本的 adb。更多信息请参考 [这篇 Stack Overflow 文章][error-device-offline]。

2. 当手机询问是否允许具有指定 RSA 密钥的计算机访问设备时，你回答了“是”。

重试之前先执行 `killall -9 adb; fusermount -u /media/mount/path`。

[enable-usb-debug]: http://www.droidviews.com/how-to-enable-developer-optionsusb-debugging-mode-on-devices-with-android-4-2-jelly-bean/
[error-device-offline]: http://stackoverflow.com/questions/10680417/error-device-offline

## 致谢

感谢原作者 **spion** 创造了这个超棒的工具。
```
