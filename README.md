# tsocks
**a transparent SOCKS proxying library (for Mac)**

This project is originally hosted by sourceforge http://tsocks.sourceforge.net

Porting to macOS by Zou Guangxian <zouguangxian@163.com> based on http://marc-abramowitz.com/archives/2006/01/29/building-tsocks-on-mac-os-x, with fixes by Mikhail Zakharov <zmey20000@yahoo.com>

## Install
```
    $ git clone https://github.com/ArioWei/tsocks.git
    $ cd tsocks
    $ autoconf -f
    $ ./configure --prefix=/usr/local --libdir=/usr/local/lib --with-conf=/usr/local/etc/tsocks.conf --enable-debug
    $ make
    $ make install
```
## Usage
```
    $ grep '^[^#]' /usr/local/etc/tsocks.conf 
    local = 192.168.0.0/255.255.0.0
    local = 172.16.0.0/255.240.0.0
    local = 10.0.0.0/255.0.0.0
    server = 127.0.0.1
    server_type = 5
    server_port = 8135

    $ TSOCKS_DEBUG=2 tsocks git pull
```
如果没有tsocks.conf，手动创建
```
    touch /usr/local/etc/tsocks.conf
```
编辑该文件，输入以下内容
```
    server = 127.0.0.1
    server_type = 5
    server_port = 8135
```
使用方法
```
    $ tsocks 命令/脚本
```
or
```
    $ source /usr/local/bin/tsocks on 
    $ telnet example.org
```
or
```
    $ . /usr/local/bin/tsocks on 
    $ telnet example.org
```

## Notes for macOS

* Install OpenSSH from sources (or use Homebrew https://brew.sh port) as the default ssh will not work with the preloaded library:
```
    brew install openssh
```

*  To permanently sockify all connections using preloaded library, set essential environmental variables on login:
```
    launchctl setenv DYLD_FORCE_FLAT_NAMESPACE 1
    launchctl setenv DYLD_INSERT_LIBRARIES /usr/local/lib/libtsocks.dylib
```
