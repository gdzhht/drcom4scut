# drcom4scut

> 当前版本  0.2.0

+ A 3rd DrCOM client for SCUT, written by Rust.
+ 华南理工大学第三方客户端，使用Rust语言编写。

------------------------------------------------------

## 用法

1. 下载 Release 并解压。
2. 运行 run.bat，第一次会产生配置文件。
   + 你也可以直接在 drcom4scut.exe 后面加参数来运行，详情请用 -h 参数获取帮助。
3. 填写配置文件，通常只需要填写 `username` 和 `password` 两项（注意yml文件格式）。
4. 再次运行 run.bat，通常是可以正常运行的。
   + 如果不能，请查看控制台输出的提示。
     + 如果没有自动选择正确的网卡，请在配置文件或控制台参数中填写 `mac` 或 `ip` 任意一项。其中 `mac` 是以冒号分隔的形式， `ip` 是你指定网卡对应设置的IP地址。
     + 如果出现不能读取配置文件，请检查填写的配置文件是否满足yml规范。

------------------------------------------------------

## 命令行参数

```bash
USAGE:
    drcom4scut.exe [FLAGS] [OPTIONS]

FLAGS:
        --debug      Enable debug mode.
    -h, --help       Prints help information
        --noudp      Disable UDP Process.
    -V, --version    Prints version information

OPTIONS:
    -c, --config <config>        (Optional) Path to config file. Some settings only can be set by config file.
    -d, --dns <dns>              (Optional) DNS server. If more than one, you can add the remain DNS servers to config
                                 file.
    -H, --host <host>            (Optional) Host to connect UDP server. Default value is 's.scut.edu.cn'.
    -N, --hostname <hostname>    (Optional) Default value is current computer host name.
    -i, --ip <ip>                (Optional) IP address of the selected Ethernet Device.
    -m, --mac <mac>              (Optional) Ethernet Device MAC address.
    -p, --password <password>    Password to authorize.
    -t, --time <time>            (Optional) Time to reconnect automatically after you are not allowed to access
                                 Internet. Default value is 7:00.
    -u, --username <username>    Username to authorize.
```

------------------------------------------------------

## 配置项

```yml
mac:   # (可选)网卡MAC地址，以冒号':'分隔
ip:   # (可选)网卡对应设置的IP地址
username: ''  # 账号（学号）
password: ''  # 密码
dns:   # 学校DNS服务器IP地址，默认已填入五山校区和大学城校区的DNS
  - 202.38.193.33
  - 222.201.130.30
  - 202.112.17.33
  - 222.201.130.33
host: s.scut.edu.cn   # (可选) 用于UDP连接的地址，通常不需要改动
hostname:   # (可选) 主机名，留空会使用当前电脑的主机名
time: 7:00   # (可选) 主机名，留空会使用当前电脑的主机名
reconnect: 60   # (可选) 主机名，留空会使用当前电脑的主机名
heartbeat:
  eap_timeout: 60   # (可选) EAP连接心跳间隔
  udp_timeout: 12   # (可选) UDP连接心跳间隔
retry:
  count: 2   # (可选) 错误重试次数
  interval: 5000   # (可选) 数据包重发间隔、错误重试间隔
log:
  directory: ./logs   # (可选) 日志目录
  level: INFO   # (可选) 日志等级
data:   # (可选) 以下参数通常不需要填写，填写错误可能会导致不可预计的问题
  response_identity:
    unknown:
  response_md5_challenge:
    unknown:
  misc_info:
    unknown1:
    crc32_param:
    unknown2:
    os_major:
    os_minor:
    os_build:
    os_unknown:
    version:
    hash:
```

------------------------------------------------------

## 构建和编译

+ 需要使用 *Nightly* 版本的 Rust 进行编译。

+ 由于使用了 [**libpnet**](https://crates.io/crates/pnet) ，在Windows下需要安装 *WinPcap* 或 *pcap* 才能进行编译，详见[**libpnet**](https://crates.io/crates/pnet)。

+ 目前只在 Windows 下编译通过，其余环境暂未测试。

------------------------------------------------------

## 许可证

[![LGPLv3](https://img.shields.io/badge/License-LGPLv3-blue.svg?longCache=true)](https://github.com/SeaLoong/drcom4scut/blob/master/LICENSE)
