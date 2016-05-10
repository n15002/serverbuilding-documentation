
kyouya [10:53 AM] 
5/10 Unix/AWSの作業手順
htps://github.com/cloneko/serverbuilding (edited)

[10:57] 
virtualboxのインストール
公式サイト https://www.virtualbox.org/wiki/Linux_Downloads
AMD64選択 ダウロード (edited)

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
vagrantのインストール
公式サイト https://www.vagrantup.com/downloads.html
debian 64bit選択 ダウンロード

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
https://github.com/cloneko/serverbuilding/blob/master/Section1.md

[11:08] 
ホストオンリーアダプタが未選択状態で設定することが出来ない。
これで解決 http://tyoimemo.blogspot.jp/2012/03/blog-post.html
