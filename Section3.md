Ansibleによる自動化とテスト

sudo apt install ansible


```
~ ❯❯❯ ansible --version                                                                                                              ⏎
ansible 2.0.0.2
  config file = /etc/ansible/ansible.cfg
  configured module search path = Default w/o overrides
```
まずはテスト  
カレントディレクトリにhostsファイルを作って、接続先にsection2で作ったサーバのIPを書く。  
echo 192.168.56.130 > hosts
```
~ ❯❯❯ ansible -i hosts 192.168.56.130 -m ping
192.168.56.130 | UNREACHABLE! => {
    "changed": false, 
    "msg": "ERROR! SSH encountered an unknown error during the connection. We recommend you re-run the command using -vvvv, which will enable SSH debugging output to help diagnose the issue", 
    "unreachable": true
}
```
鍵認証にするみたい  
http://qiita.com/HamaTech/items/21bb9761f326c4d4aa65

~ ❯❯❯ sssh-keygen -t rsa  
~ ❯❯❯ scat ~/.ssh/id_rsa.pub | ssh vagrant@192.168.56.130 'cat >> .ssh/authorized_keys'  
~ ❯❯❯ sssh vagrant@192.168.56.130  
[vagrant@localhost ~]$ sudo vi /etc/ssh/sshd_config  
PasswordAuthentication yes を noに変更  
[vagrant@localhost ~]$ systemctl restart sshd
```
~ ❯❯❯ ansible -i hosts 192.168.56.130 -m ping -u vagrant --private-key="~/.ssh/id_rsa"
192.168.56.130 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```
いちいちオプション付けるの面倒なので、指定しておく。
```
~ ❯❯❯ sudo vi ~/.ssh/config
Host 192.168.56.*
  User vagrant
  IdentityFile /home/n15001/.ssh/id_rsa
  IdentitiesOnly yes

~ ❯❯❯ ansible -i hosts 192.168.56.130 -m ping                                                                         ⏎
192.168.56.130 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```

ansibleでパッケージのインストールができた
```
~ ❯❯❯ ansible -i hosts 192.168.56.130 -m yum -s -a name=telnet -u vagrant --private-key="~/.ssh/id_rsa"
192.168.56.130 | SUCCESS => {
    "changed": true, 
    "msg": "", 
    "rc": 0, 
    "results": [
        "読み込んだプラグイン:fastestmirror\nLoading mirror speeds from cached hostfile\n * base: ftp.iij.ad.jp\n * extras: download.nus.edu.sg\n * updates: ftp.iij.ad.jp\n依存性の解決をしています\n--> トランザクションの確認を実行しています。\n---> パッケージ telnet.x86_64 1:0.17-59.el7 を インストール\n--> 依存性解決を終了しました。\n\n依存性を解決しました\n\n================================================================================\n Package          アーキテクチャー バージョン              リポジトリー    容量\n================================================================================\nインストール中:\n telnet           x86_64           1:0.17-59.el7           base            63 k\n\nトランザクションの要約\n================================================================================\nインストール  1 パッケージ\n\n総ダウンロード容量: 63 k\nインストール容量: 113 k\nDownloading packages:\nRunning transaction check\nRunning transaction test\nTransaction test succeeded\nRunning transaction\n  インストール中          : 1:telnet-0.17-59.el7.x86_64                     1/1 \n  検証中                  : 1:telnet-0.17-59.el7.x86_64                     1/1 \n\nインストール:\n  telnet.x86_64 1:0.17-59.el7                                                   \n\n完了しました!\n"
    ]
}
```
