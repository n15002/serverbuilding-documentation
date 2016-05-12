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

cp wp-config-sample.php wp-config.php
DB名やユーザ名を書き込む

iptables使ってポートを開ける
```
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT
iptables -L
```
ブラウザかOSの設定でローカルアドレス（192.168.*）をプロキシ除外する。

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


