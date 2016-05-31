Section 1 基本のサーバー構築
=====
https://github.com/cloneko/serverbuilding/blob/master/Section1.md

1-1 CentOS 7のインストール
-----
ターミナルでvirtualboxと打つか、ダッシュボードから検索して起動する。
タブの新規からCentOS7のISOファイルを選択し、仮想マシンを作成する。

ホストオンリーアダプタが未選択状態で設定することが出来ない。  
これで解決 http://tyoimemo.blogspot.jp/2012/03/blog-post.html  

パソコンに右Ctrlが無いので、**環境設定**からホストキーを左Ctrl+Shiftに変更する。  
isoを指定して起動順番をディスク＞HDDに変更  
プロセッサーを2CPUに変更して80%使用率制限した  

**/etc/sysconfig/network-scriptにifcfg-enp0s?**にはデフォルトでインターフェースごとにDHCPと書いてあるので、ONBOOTをyesに書き換え、
`service network restart`で`ip a`でIP確認してから、母機から`ssh vagrant@確認したIP`で接続する。（パスワードもvagrant）

1-2 Wordpressを動かす(1)
-----
proxyの設定  
```
sudo vi /etc/yum.conf  
proxy = http://172.16.40.1:8888 #書き換える

sudo vi /etc/wgetrc
http_proxy = http://172.16.40.1:8888 #書き換える
https_proxy = https://172.16.40.1:8888 #書き換える
```
~~IPv6が邪魔してたので停止させる  
http://orebibou.com/2014/12/centos-7%E3%81%A7ipv6%E3%82%92%E7%84%A1%E5%8A%B9%E5%8C%96%E3%81%99%E3%82%8B/~~  
邪魔してなかったけど、とりあえずやっておこう。

yumのアップデートを行い、**apache**や**php**、また**wordpress**本体をダウンロードする為にwgetもインストールする。
```
sudo yum update
sudo yum install httpd php php-mysql wget
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

**http://CentOSのIP/wordpress**へアクセスする。　
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
