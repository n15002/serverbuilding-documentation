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

prefixつけたほうがいいのかも
```
[vagrant@localhost httpd-2.2.31]$ sudo /usr/local/apache2/bin/apachectl -v
Server version: Apache/2.2.31 (Unix)
Server built:   May 19 2016 17:21:16
[vagrant@localhost httpd-2.2.31]$ sudo ps -aux |grep -i httpd
root     12178  0.0  0.1  27768  1644 ?        Ss   17:34   0:00 /usr/local/apache2/bin/httpd -k start
daemon   12179  0.0  0.1  27768  1140 ?        S    17:34   0:00 /usr/local/apache2/bin/httpd -k start
daemon   12180  0.0  0.1  27904  1796 ?        S    17:34   0:00 /usr/local/apache2/bin/httpd -k start
daemon   12181  0.0  0.1  27768  1140 ?        S    17:34   0:00 /usr/local/apache2/bin/httpd -k start
daemon   12182  0.0  0.1  27768  1140 ?        S    17:34   0:00 /usr/local/apache2/bin/httpd -k start
daemon   12183  0.0  0.1  27768  1140 ?        S    17:34   0:00 /usr/local/apache2/bin/httpd -k start
daemon   12223  0.0  0.1  27768  1144 ?        S    17:49   0:00 /usr/local/apache2/bin/httpd -k start
```
![apache2.2いんすこ画像](https://raw.githubusercontent.com/n15001/serverbuilding-documentation/master/Screenshot%20from%202016-05-19%2018-11-24.png "apache2.2いんすこ画像")

modrewite入ってなかった
```
[vagrant@localhost ~]$ sudo /usr/local/apache2/bin/apxs -i -a -c ~/httpd-2.2.31/modules/mappers/mod_rewrite.c
/usr/local/apache2/build/libtool --silent --mode=compile gcc -prefer-pic   -DLINUX -D_REENTRANT -D_GNU_SOURCE -g -O2 -pthread -I/usr/local/apache2/include  -I/usr/local/apache2/include   -I/usr/local/apache2/include   -c -o /home/vagrant/httpd-2.2.31/modules/mappers/mod_rewrite.lo /home/vagrant/httpd-2.2.31/modules/mappers/mod_rewrite.c && touch /home/vagrant/httpd-2.2.31/modules/mappers/mod_rewrite.slo
/usr/local/apache2/build/libtool --silent --mode=link gcc -o /home/vagrant/httpd-2.2.31/modules/mappers/mod_rewrite.la  -rpath /usr/local/apache2/modules -module -avoid-version    /home/vagrant/httpd-2.2.31/modules/mappers/mod_rewrite.lo
/usr/local/apache2/build/instdso.sh SH_LIBTOOL='/usr/local/apache2/build/libtool' /home/vagrant/httpd-2.2.31/modules/mappers/mod_rewrite.la /usr/local/apache2/modules
/usr/local/apache2/build/libtool --mode=install cp /home/vagrant/httpd-2.2.31/modules/mappers/mod_rewrite.la /usr/local/apache2/modules/
cp /home/vagrant/httpd-2.2.31/modules/mappers/.libs/mod_rewrite.so /usr/local/apache2/modules/mod_rewrite.so
cp /home/vagrant/httpd-2.2.31/modules/mappers/.libs/mod_rewrite.lai /usr/local/apache2/modules/mod_rewrite.la
cp /home/vagrant/httpd-2.2.31/modules/mappers/.libs/mod_rewrite.a /usr/local/apache2/modules/mod_rewrite.a
chmod 644 /usr/local/apache2/modules/mod_rewrite.a
ranlib /usr/local/apache2/modules/mod_rewrite.a
PATH="$PATH:/sbin" ldconfig -n /usr/local/apache2/modules
----------------------------------------------------------------------
Libraries have been installed in:
   /usr/local/apache2/modules

If you ever happen to want to link against installed libraries
in a given directory, LIBDIR, you must either use libtool, and
specify the full pathname of the library, or use the `-LLIBDIR'
flag during linking and do at least one of the following:
   - add LIBDIR to the `LD_LIBRARY_PATH' environment variable
     during execution
   - add LIBDIR to the `LD_RUN_PATH' environment variable
     during linking
   - use the `-Wl,--rpath -Wl,LIBDIR' linker flag
   - have your system administrator add LIBDIR to `/etc/ld.so.conf'

See any operating system documentation about shared libraries for
more information, such as the ld(1) and ld.so(8) manual pages.
----------------------------------------------------------------------
chmod 755 /usr/local/apache2/modules/mod_rewrite.so
[activating module `rewrite' in /usr/local/apache2/conf/httpd.conf]
[vagrant@localhost ~]$ ls /usr/local/apache2/modules/
httpd.exp       mod_rewrite.so 
```
libphp7.soが入ってなかったのでコピペで再ビルド  
http://qiita.com/ssaita/items/9e0170251d45ed1b8818

configure: error: xpm.h not found.  
yum install libXpm-devel.x86_64  
configure: error: Unable to locate gmp.h  
yum install gmp-devel 

mysql_config not found  
configure: error: Please reinstall the mysql distribution  
[vagrant@localhost php-src]$ mysql_config  
-bash: mysql_config: コマンドが見つかりません  
[vagrant@localhost php-src]$ sudo yum install mariadb-devel -y  
[vagrant@localhost php-src]$ which mysql_config  
/usr/bin/mysql_config  
configure: error: Cannot find pspell

```
[vagrant@localhost php-src]$ sudo make install
Installing PHP SAPI module:       apache2handler
/usr/local/apache2/build/instdso.sh SH_LIBTOOL='/usr/local/apache2/build/libtool' libphp7.la /usr/local/apache2/modules
/usr/local/apache2/build/libtool --mode=install cp libphp7.la /usr/local/apache2/modules/
cp .libs/libphp7.so /usr/local/apache2/modules/libphp7.so
cp .libs/libphp7.lai /usr/local/apache2/modules/libphp7.la
libtool: install: warning: remember to run `libtool --finish /home/vagrant/php-src/libs'
chmod 755 /usr/local/apache2/modules/libphp7.so
[activating module `php7' in /usr/local/apache2/conf/httpd.conf]
Installing shared extensions:     /usr/local/lib/php/extensions/no-debug-non-zts-20151012/
Installing PHP CLI binary:        /usr/local/bin/
Installing PHP CLI man page:      /usr/local/php/man/man1/
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
[PEAR] Archive_Tar    - already installed: 1.4.0
[PEAR] Console_Getopt - already installed: 1.4.1
[PEAR] Structures_Graph- already installed: 1.1.1
[PEAR] XML_Util       - already installed: 1.3.0
[PEAR] PEAR           - already installed: 1.10.1
Wrote PEAR system config file at: /usr/local/etc/pear.conf
You may want to add: /usr/local/lib/php to your php.ini include_path
/home/vagrant/php-src/build/shtool install -c ext/phar/phar.phar /usr/local/bin
ln -s -f phar.phar /usr/local/bin/phar
Installing PDO headers:          /usr/local/include/php/ext/pdo/
[vagrant@localhost php-src]$ php -v
PHP 7.0.2 (cli) (built: May 19 2016 20:19:36) ( NTS )
Copyright (c) 1997-2015 The PHP Group
Zend Engine v3.0.0, Copyright (c) 1998-2015 Zend Technologies

[vagrant@localhost php-src]$ ls /usr/local/apache2/modules/
httpd.exp       libphp7.so      mod_rewrite.so  

```
sudo vi /usr/local/apache2/conf/httpd.conf  
LoadModule php7_module  modules/libphp7.soがあるか確認する、無ければ書く。  
DocumentRoot "/usr/local/apache2/htdocs/wordpress/"と書き足す  
AddType application/x-httpd-php .phpと  
DirectoryIndex にindex.phpを追加する  
sudo /usr/local/apache2/bin/httpd -k restart  

wordpressをwgetしてデータベース作ってconfig書いて自分のIPにアクセスしてはいちゅんちゅん(・8・)  

![wordpressがめん](https://raw.githubusercontent.com/n15001/serverbuilding-documentation/master/Screenshot%20from%202016-05-19%2020-53-17.png "wordpressがめん")

abtest、100リクエスト全部捌けてるっぽい。
```
~ ❯❯❯ sudo ab -n 100 -c 100 http://192.168.56.130/                                                                                   ⏎
[sudo] password for n15001: 
This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/
Benchmarking 192.168.56.130 (be patient).....done

Server Software:        Apache/2.2.31
Server Hostname:        192.168.56.130
Server Port:            80

Document Path:          /
Document Length:        263 bytes

Concurrency Level:      100
Time taken for tests:   102.097 seconds
Complete requests:      100
Failed requests:        0
Non-2xx responses:      100
Total transferred:      59400 bytes
HTML transferred:       26300 bytes
Requests per second:    0.98 [#/sec] (mean)
Time per request:       102097.003 [ms] (mean)
Time per request:       1020.970 [ms] (mean, across all concurrent requests)
Transfer rate:          0.57 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        8   20   7.8     21      33
Processing: 26725 56369 19722.1  57032  102087
Waiting:    26058 56072 19845.0  57032  102067
Total:      26733 56389 19728.6  57046  102096

Percentage of the requests served within a certain time (ms)
  50%  57046
  66%  71397
  75%  73806
  80%  79396
  90%  80626
  95%  81247
  98%  96518
  99%  102096
 100%  102096 (longest request)
```
PageSpeed Insightsは78/100点
セクション2.2のサーバと同じような事が書いてた

とりあえずセキュリティチェック
ノパソ本体（ubuntu16.04）にOpenVasのインストール
https://launchpad.net/~mrazavi/+archive/ubuntu/openvas
```
sudo vi /etc/apt/sources.list
deb http://ppa.launchpad.net/mrazavi/openvas/ubuntu YOUR_UBUNTU_VERSION_HERE main を追加
sudo apt update
~/k/openvas ❯❯❯ sudo apt-cache search openvas                                                                           ⏎
openvas-scanner - remote network security auditor - scanner
openvas-cli - remote network security auditor - cli
openvas-manager - remote network security auditor - manager
openvas - remote network security auditor - metapackage
libopenvas8-dev - remote network security auditor - static libraries and headers
libopenvas8 - remote network security auditor - shared libraries
openvas-gsa - remote network security auditor - web interface
libopenvas9-dev - remote network security auditor - static libraries and headers
libopenvas9 - remote network security auditor - shared libraries
openvas9-scanner - remote network security auditor - scanner
openvas9-manager - remote network security auditor - manager
openvas9 - remote network security auditor - metapackage
openvas9-cli - remote network security auditor - cli
openvas9-gsa - remote network security auditor - web interface
sudo apt install openvas -y
```
sudo service openvas-scanner status
sudo service openvas-manager status
https://localhostにアクセスする
ユーザ名:admin password:admin
オレオレ警告が出るけど”このURLにアクセスする”を選択

nmap
```
~/k/openvas ❯❯❯ sudo nmap -A 192.168.56.130
Starting Nmap 7.01 ( https://nmap.org ) at 2016-05-20 09:50 JST
Nmap scan report for 192.168.56.130
Host is up (0.0027s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 6.6.1 (protocol 2.0)
| ssh-hostkey: 
|   2048 99:46:8f:89:7a:61:15:60:75:3b:b3:76:8e:e3:5f:e5 (RSA)
|_  256 a6:42:51:74:ea:0d:da:92:6f:c8:0b:3b:37:8a:f5:5b (ECDSA)
80/tcp   open  http    Apache httpd 2.2.31 ((Unix) PHP/7.0.2)
|_http-generator: WordPress 4.5.2
|_http-server-header: Apache/2.2.31 (Unix) PHP/7.0.2
|_http-title: n15001\xE3\x81\xAE\xE3\x81\xB6\xE3\x82\x8D\xE3\x81\x90 &#8211; Just another WordPress site
3306/tcp open  mysql   MariaDB (unauthorized)
MAC Address: 08:00:27:32:BB:52 (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.0
Network Distance: 1 hop

TRACEROUTE
HOP RTT     ADDRESS
1   2.74 ms 192.168.56.130

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.02 seconds
```
