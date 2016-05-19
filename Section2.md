Stderr: VBoxManage: error: Implementation of the USB 2.0 controller not found!~ なエラーが出る。  
拡張機能をここからダウンロードして追加する  
https://www.virtualbox.org/wiki/Downloads  

Section 2 その他のWebサーバー環境  
------
```
~/hoge ❯❯❯  vagrant up                                                                                               ⏎
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Clearing any previously set forwarded ports...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: Warning: Remote connection disconnect. Retrying...
    default: Warning: Remote connection disconnect. Retrying...
    default: Warning: Remote connection disconnect. Retrying...
    default: Warning: Remote connection disconnect. Retrying...
    default: 
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default: 
    default: Inserting generated public key within guest...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Mounting shared folders...
    default: /vagrant => /home/n15001/hoge
~/hoge ❯❯❯ ssh -p 2222 vagrant@127.0.0.1
The authenticity of host '[127.0.0.1]:2222 ([127.0.0.1]:2222)' can't be established.
ECDSA key fingerprint is SHA256:UnxXQA40hJNUe2z4urc65UcMPnwFatSmVGrSCt69EMY.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[127.0.0.1]:2222' (ECDSA) to the list of known hosts.
vagrant@127.0.0.1's password: 
Last login: Wed May 11 10:18:14 2016
[vagrant@localhost ~]$
```

http://www.server-memo.net/memo/wordpress/nginx-install.html  

sudo vi /etc/yum.conf  
sudo vi /etc/wgetrc

systemctl enable mysql  
systemctl restart nginx  
systemctl status nginx  
sudo nginx -t  
sudo vi /etc/nginx/nginx.conf

トップページだけ403になって謎だった  
indexディレクティブを書かないとダメ  
http://stackoverflow.com/questions/27093823/403-forbidden-error-in-nginx-configuration-for-wordpress-site  
2-2はできた  

abてすとくそでわ  
```
~ ❯❯❯ ab -n 100 -c 100 http://192.168.56.129/                                                                          ⏎
This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/
Benchmarking 192.168.56.129 (be patient).....done

Server Software:        nginx/1.6.3
Server Hostname:        192.168.56.129
Server Port:            80

Document Path:          /
Document Length:        11976 bytes

Concurrency Level:      100
Time taken for tests:   93.164 seconds
Complete requests:      100
Failed requests:        55
   (Connect: 0, Receive: 0, Length: 55, Exceptions: 0)
Non-2xx responses:      55
Total transferred:      567665 bytes
HTML transferred:       548160 bytes
Requests per second:    1.07 [#/sec] (mean)
Time per request:       93163.859 [ms] (mean)
Time per request:       931.639 [ms] (mean, across all concurrent requests)
Transfer rate:          5.95 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       10   20   6.4     21      29
Processing: 11563 63666 20085.8  63902   93153
Waiting:     9217 54076 16046.5  60379   66176
Total:      11573 63686 20086.8  63929   93163

Percentage of the requests served within a certain time (ms)
  50%  63929
  66%  65492
  75%  81663
  80%  84156
  90%  87241
  95%  88419
  98%  91191
  99%  93163
 100%  93163 (longest request)
```
2日目にvagrant up したらエラーはいた  
```
Failed to mount folders in Linux guest. This is usually because
the "vboxsf" file system is not available. Please verify that
the guest additions are properly installed in the guest and
can work properly. The command attempted was:

mount -t vboxsf -o uid=`id -u vagrant`,gid=`getent group vagrant | cut -d: -f3` vagrant /vagrant
mount -t vboxsf -o uid=`id -u vagrant`,gid=`id -g vagrant` vagrant /vagrant

The error output from the last command was:

/sbin/mount.vboxsf: mounting failed with the error: No such devic
```
共有フォルダ作ってたみたいなのでそれが原因、vagrant用プラグインvagrant-vbguestを入れる。
http://qiita.com/akippiko/items/278efedee35661634b85

```
~/kaihatu ❯❯❯ vagrant plugin install vagrant-vbguest
Installing the 'vagrant-vbguest' plugin. This can take a few minutes...
Installed the plugin 'vagrant-vbguest (0.11.0)'!
~/kaihatu ❯❯❯ vagrant up                                                                                                             ⏎
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Clearing any previously set forwarded ports...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
    default: Adapter 2: hostonly
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: Warning: Remote connection disconnect. Retrying...
    default: Warning: Remote connection disconnect. Retrying...
    default: Warning: Remote connection disconnect. Retrying...
    default: Warning: Remote connection disconnect. Retrying...
==> default: Machine booted and ready!
No installation found.
Package kernel-devel-3.10.0-327.18.2.el7.x86_64 already installed and latest version
Package gcc-4.8.5-4.el7.x86_64 already installed and latest version
Package 1:make-3.82-21.el7.x86_64 already installed and latest version
Package 4:perl-5.16.3-286.el7.x86_64 already installed and latest version
Package bzip2-1.0.6-13.el7.x86_64 already installed and latest version
Nothing to do
Copy iso file /usr/share/virtualbox/VBoxGuestAdditions.iso into the box /tmp/VBoxGuestAdditions.iso
mount: /dev/loop0 is write-protected, mounting read-only
Installing Virtualbox Guest Additions 5.0.20 - guest version is unknown
Verifying archive integrity... All good.
Uncompressing VirtualBox 5.0.20 Guest Additions for Linux............
VirtualBox Guest Additions installer
Removing installed version 5.0.20 of VirtualBox Guest Additions...
Removing existing VirtualBox non-DKMS kernel modules[  OK  ]
Copying additional installer modules ...
Installing additional modules ...
Removing existing VirtualBox non-DKMS kernel modules[  OK  ]
Building the VirtualBox Guest Additions kernel modules
Building the main Guest Additions module[  OK  ]
Building the shared folder support module[  OK  ]
Building the graphics driver module[  OK  ]
Doing non-kernel setup of the Guest Additions[  OK  ]
Starting the VirtualBox Guest Additions Installing the Window System drivers
Could not find the X.Org or XFree86 Window System, skipping.
[  OK  ]
==> default: Checking for guest additions in VM...
==> default: Configuring and enabling network interfaces...
==> default: Mounting shared folders...
    default: /vagrant => /home/n15001/kaihatu
==> default: Machine already provisioned. Run `vagrant provision` or use the `--provision`
==> default: flag to force provisioning. Provisioners marked to run always will still run.
~/kaihatu ❯❯❯  vagrant vbguest --status
GuestAdditions 5.0.20 running --- OK.
```
PageSpeed Insights (with PNaCl)  
https://chrome.google.com/webstore/detail/pagespeed-insights-with-p/lanlbpjbalfkflkhegagflkgcfklnbnh?hl=ja  

僕の環境chromiumじゃ動かなかった、純chromeじゃないとダメらしい。
点数：78/100  
jqueryなんかを圧縮してサイズ減らせって書いてあった  


PHP7.0.2のインストール
------
公式サイト：http://php.net/manual/ja/migration70.php
```
sudo vi ~/.gitconfig
[http]  
    proxy = http://学校のプロキシ:ぽーと
[https] 
    proxy = https://学校のプロキシ:ポート

git clone -b PHP-7.0.2 https://github.com/php/php-src.git
yum install autoconf
[vagrant@localhost php-src]$ ./buildconf --force
[vagrant@localhost php-src]$ ./configure --help 
[vagrant@localhost php-src]$ ./configure --with-zlib-dir --with-freetype-dir --enable-mbstring --with-libxml-dir=--enable-soap --enable-calendar --with-curl --with-mcrypt --with-zlib --with-gd --disable-rpath --enable-inline-optimization --with-bz2 --with-zlib --enable-sockets --enable-sysvsem --enable-sysvshm --enable-pcntl --enable-mbregex --enable-exif --enable-bcmath --with-mhash --enable-zip --with-pcre-regex --with-pdo-mysql --with-mysqli --with-mysql-sock=/var/run/mysqld/mysqld.sock --with-jpeg-dir=/usr --with-png-dir=/usr --enable-gd-native-ttf --with-openssl --with-fpm-user=USER --with-fpm-group=USER --with-libdir --enable-ftp --with-kerberos --with-gettext --with-xmlrpc --with-xsl --enable-opcache --enable-fpm
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking for a sed that does not truncate output... /usr/bin/sed
checking build system type... x86_64-unknown-linux-gnu
checking host system type... x86_64-unknown-linux-gnu
checking target system type... x86_64-unknown-linux-gnu
checking for cc... cc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether cc accepts -g... yes
checking for cc option to accept ISO C89... none needed
checking how to run the C preprocessor... cc -E
checking for icc... no
checking for suncc... no
checking whether cc understands -c and -o together... yes
checking how to run the C preprocessor... cc -E
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for unistd.h... yes
checking minix/config.h usability... no
checking minix/config.h presence... no
checking for minix/config.h... no
checking whether it is safe to define __EXTENSIONS__... yes
checking whether ln -s works... yes
checking for system library directory... yes
checking whether to enable runpaths... no
checking if compiler supports -R... no
checking if compiler supports -Wl,-rpath,... yes
checking for gawk... gawk
checking for bison... no
checking for byacc... no
checking for bison version... invalid
configure: WARNING: This bison version is not supported for regeneration of the Zend/PHP parsers (found: none, min: 204, excluded: ).
checking for re2c... no
configure: WARNING: You will need re2c 0.13.4 or later if you want to regenerate PHP parsers.
configure: error: bison is required to build PHP/Zend when building a GIT checkout!

wget http://downloads.sourceforge.net/project/re2c/0.16/re2c-0.16.tar.gz
tar zxvf re2c-0.16.tar.gz
cd re2c-0.16
./configure
G++が見つかりません
yum install gcc-c++
make

sudo yum install bison

再びconfigureでエラー：configure: error: mcrypt.h not found. Please reinstall libmcrypt.

sudo yum install epel-release
sudo vi /etc/yum.repos.d/epel.repo →enabled=1を0に変更して明示的にー
sudo yum --enablerepo=epel install libmcrypt-devel

make
permission errorが出たのでsudo付けてmake install
[vagrant@localhost php-src]$ sudo make install
Installing shared extensions:     /usr/local/lib/php/extensions/no-debug-non-zts-20151012/
Installing PHP CLI binary:        /usr/local/bin/
Installing PHP CLI man page:      /usr/local/php/man/man1/
Installing PHP FPM binary:        /usr/local/sbin/
Installing PHP FPM config:        /usr/local/etc/
Installing PHP FPM man page:      /usr/local/php/man/man8/
Installing PHP FPM status page:      /usr/local/php/php/fpm/
Installing phpdbg binary:         /usr/local/bin/
Installing phpdbg man page:       /usr/local/php/man/man1/
Installing PHP CGI binary:        /usr/local/bin/
Installing PHP CGI man page:      /usr/local/php/man/man1/
Installing build environment:     /usr/local/lib/php/build/
Installing header files:          /usr/local/include/php/
Installing helper programs:       /usr/local/bin/
  program: phpize
  program: php-config
Installing man pages:             /usr/local/php/man/man1/
  page: phpize.1
  page: php-config.1
Installing PEAR environment:      /usr/local/lib/php/
--2016-05-19 16:49:51--  https://pear.php.net/install-pear-nozlib.phar
学校のプロキシ:ぽーと に接続しています... 接続しました。
Proxy による接続要求を送信しました、応答を待っています... 200 OK
長さ: 3579275 (3.4M) [text/plain]
`pear/install-pear-nozlib.phar' に保存中

100%[=============================================================================================>] 3,579,275    720KB/s 時間 5.1s   

2016-05-19 16:49:58 (681 KB/s) - `pear/install-pear-nozlib.phar' へ保存完了 [3579275/3579275]

[PEAR] Archive_Tar    - installed: 1.4.0
[PEAR] Console_Getopt - installed: 1.4.1
[PEAR] Structures_Graph- installed: 1.1.1
[PEAR] XML_Util       - installed: 1.3.0
[PEAR] PEAR           - installed: 1.10.1
Wrote PEAR system config file at: /usr/local/etc/pear.conf
You may want to add: /usr/local/lib/php to your php.ini include_path
/home/vagrant/php-src/build/shtool install -c ext/phar/phar.phar /usr/local/bin
ln -s -f phar.phar /usr/local/bin/phar
Installing PDO headers:          /usr/local/include/php/ext/pdo/
$ php -v
PHP 7.0.2 (cli) (built: May 19 2016 16:45:06) ( NTS )
Copyright (c) 1997-2015 The PHP Group
Zend Engine v3.0.0, Copyright (c) 1998-2015 Zend Technologies
```
apache2.2のインストール
------
wget http://ftp.kddilabs.jp/infosystems/apache//httpd/httpd-2.2.31.tar.gz  
tar zxvf httpd-2.2.31.tar.gz  
cd httpd-2.2.31  
./configure  
make  
sudo make install


