5/10 Unix/AWSの作業手順
======
https://github.com/cloneko/serverbuilding

###virtualboxのインストール
公式サイト：https://www.virtualbox.org/wiki/Linux_Downloads  
AMD64を選択してダウンロード
```
~/Downloads ❯❯❯ sudo dpkg -i virtualbox-5.0_5.0.20-106931-Ubuntu-xenial_amd64.deb
[sudo] password for n15001: 
以前に未選択のパッケージ virtualbox-5.0 を選択しています。
(データベースを読み込んでいます ... 現在 166985 個のファイルとディレクトリがインストールされています。)
virtualbox-5.0_5.0.20-106931-Ubuntu-xenial_amd64.deb を展開する準備をしています ...
virtualbox-5.0 (5.0.20-106931~Ubuntu~xenial) を展開しています...
dpkg: 依存関係の問題により virtualbox-5.0 の設定ができません:
 virtualbox-5.0 は以下に依存 (depends) します: libqt4-opengl (>= 4:4.7.2) ...しかし:
  パッケージ libqt4-opengl はまだインストールされていません。
​
dpkg: パッケージ virtualbox-5.0 の処理中にエラーが発生しました (--install):
 依存関係の問題 - 設定を見送ります
ureadahead (0.100.0-19) のトリガを処理しています ...
ureadahead will be reprofiled on next reboot
systemd (229-4ubuntu4) のトリガを処理しています ...
hicolor-icon-theme (0.15-0ubuntu1) のトリガを処理しています ...
shared-mime-info (1.5-2) のトリガを処理しています ...
gnome-menus (3.13.3-6ubuntu3) のトリガを処理しています ...
desktop-file-utils (0.22-1ubuntu5) のトリガを処理しています ...
mime-support (3.59ubuntu1) のトリガを処理しています ...
処理中にエラーが発生しました:
 virtualbox-5.0
~/Downloads ❯❯❯ sudo apt install libqt4-opengl                                                                                       ⏎
パッケージリストを読み込んでいます... 完了
依存関係ツリーを作成しています                
状態情報を読み取っています... 完了
以下のパッケージが新たにインストールされます:
  libqt4-opengl
アップグレード: 0 個、新規インストール: 1 個、削除: 0 個、保留: 35 個。
1 個のパッケージが完全にインストールまたは削除されていません。
301 kB のアーカイブを取得する必要があります。
この操作後に追加で 1,251 kB のディスク容量が消費されます。
取得:1 http://jp.archive.ubuntu.com/ubuntu xenial/main amd64 libqt4-opengl amd64 4:4.8.7+dfsg-5ubuntu2 [301 kB]
301 kB を 14秒 で取得しました (20.5 kB/s)                                                                                             
以前に未選択のパッケージ libqt4-opengl:amd64 を選択しています。
(データベースを読み込んでいます ... 現在 167759 個のファイルとディレクトリがインストールされています。)
.../libqt4-opengl_4%3a4.8.7+dfsg-5ubuntu2_amd64.deb を展開する準備をしています ...
libqt4-opengl:amd64 (4:4.8.7+dfsg-5ubuntu2) を展開しています...
libc-bin (2.23-0ubuntu3) のトリガを処理しています ...
libqt4-opengl:amd64 (4:4.8.7+dfsg-5ubuntu2) を設定しています ...
virtualbox-5.0 (5.0.20-106931~Ubuntu~xenial) を設定しています ...
Adding group `vboxusers' (GID 129) ...
Done.
Stopping VirtualBox kernel modules ...done.
Recompiling VirtualBox kernel modules ...done.
Starting VirtualBox kernel modules ...done.
libc-bin (2.23-0ubuntu3) のトリガを処理しています ...
~/Downloads ❯❯❯ sudo dpkg -i virtualbox-5.0_5.0.20-106931-Ubuntu-xenial_amd64.deb
(データベースを読み込んでいます ... 現在 167768 個のファイルとディレクトリがインストールされています。)
virtualbox-5.0_5.0.20-106931-Ubuntu-xenial_amd64.deb を展開する準備をしています ...
virtualbox-5.0 (5.0.20-106931~Ubuntu~xenial) で (5.0.20-106931~Ubuntu~xenial に) 上書き展開しています ...
virtualbox-5.0 (5.0.20-106931~Ubuntu~xenial) を設定しています ...
addgroup: The group `vboxusers' already exists as a system group. Exiting.
Stopping VirtualBox kernel modules ...done.
Removing old VirtualBox pci kernel module ...done.
Recompiling VirtualBox kernel modules ...done.
Starting VirtualBox kernel modules ...done.
ureadahead (0.100.0-19) のトリガを処理しています ...
systemd (229-4ubuntu4) のトリガを処理しています ...
hicolor-icon-theme (0.15-0ubuntu1) のトリガを処理しています ...
shared-mime-info (1.5-2) のトリガを処理しています ...
gnome-menus (3.13.3-6ubuntu3) のトリガを処理しています ...
desktop-file-utils (0.22-1ubuntu5) のトリガを処理しています ...
mime-support (3.59ubuntu1) のトリガを処理しています ...
~/Downloads ❯❯❯ virtualbox -h                                                                                                        ⏎
Oracle VM VirtualBox Manager 5.0.20
(C) 2005-2016 Oracle Corporation
All rights reserved.
```
###vagrantのインストール
公式サイト：https://www.vagrantup.com/downloads.html  
debianの64bit選択してダウンロード  

```
~/Downloads ❯❯❯ sudo dpkg -i vagrant_1.8.1_x86_64.deb
(データベースを読み込んでいます ... 現在 174271 個のファイルとディレクトリがインストールされています。)
vagrant_1.8.1_x86_64.deb を展開する準備をしています ...
vagrant (1:1.8.1) で (1:1.8.1 に) 上書き展開しています ...
vagrant (1:1.8.1) を設定しています ...
~/Downloads ❯❯❯ vagrant -v                                                                                                           ⏎
Vagrant 1.8.1
```

Section 1 基本のサーバー構築
------
https://github.com/cloneko/serverbuilding/blob/master/Section1.md

ターミナルでvirtualboxと打つか、ダッシュボードから検索して起動する。

ホストオンリーアダプタが未選択状態で設定することが出来ない。  
これで解決 http://tyoimemo.blogspot.jp/2012/03/blog-post.html  

パソコンに右Ctrlが無いので、環境設定からホストキーを左Ctrl+Shiftに変更する。  
isoを指定して起動順番をディスク＞HDDに変更  
プロセッサーを2CPUに変更して80%使用率制限した  

デフォでインターフェースごとにDHCP書いてあったので、ONBOOTをyesにしてservice network restartでip a でIP確認してからSSHできた

proxy設定  
http://qiita.com/chidakiyo/items/95cbc263f8157cfa5cd7

~~IPv6が邪魔してたので停止させる  
http://orebibou.com/2014/12/centos-7%E3%81%A7ipv6%E3%82%92%E7%84%A1%E5%8A%B9%E5%8C%96%E3%81%99%E3%82%8B/~~  
邪魔してなかったけど、とりあえずやっておこう。

rootでyumのアップデートを行い、apacheやphp、またwordpress本体をダウンロードする為にwgetもインストールする。
```
su -
yum update
yum install httpd php php-mysql wget
```
標準でmysql-serverインストール出来ないので下を参照。  
mysql-serverのインストール: http://sawara.me/mysql/2094/  

wordpressをダウンロードし、解凍、apacheの公開ディレクトリに移動させ所有者やグループをapacheへ変更しておく。
```
wget https://ja.wordpress.org/wordpress-4.5.2-ja.tar.gz
tar zxvf wordpress-4.5.2-ja.tar.gz
sudo mv ~/wordpress /var/www/html/
chown -R apache:apache /var/www/html/wordpress/*
```

rootユーザにパスワードを設定し、wordpress用のユーザを制作、権限を与えてパスワードを設定する。
```
mysql> SELECT host,user FROM mysql.user;
mysql> SET PASSWORD FOR root@"localhost"=PASSWORD('********');
mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE ON *.* TO　n15001@"localhost" IDENTIFIED BY "********";
```

サンプルをコピーして、DB名やユーザ名を書き込む。
```
cp wp-config-sample.php wp-config.php
vi wp-config.php
```

iptables使って、Webサーバで使うポートを開ける
```
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT
iptables -L
```
ブラウザかOSの設定でローカルアドレス（192.168.*）をプロキシ除外する。  
ホストOSのブラウザからCentOSのIPへアクセスして、apacheの画面が表示される事を確認する。

http://CentOSのIP/wordpressへアクセスする。　
phpinfoは見れるがwordpressが500エラー  
phpのエラーログを表示して、原因を探る。
```
sudo vi /etc/php.ini 
display_errors = ←On
```
permissionなんとかって書かれてた

SELINUXが邪魔してたみたい、停止させておく。
```
sudo vi /etc/selinux/config
SELINUX=disabled
```

http://CentOSのIP/wordpress/wp-admin/install.phpへアクセスして、適宜書く。
![install.phpの画像](https://raw.githubusercontent.com/n15001/serverbuilding-documentation/master/1.png)

何も問題が無ければインストールが完了し、記事も投稿できるはず。  
![インストール完了画面](https://raw.githubusercontent.com/n15001/serverbuilding-documentation/master/2.png)

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

