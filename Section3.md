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
~ ❯❯❯ ansible -vvv -i hosts 192.168.56.130 -m ping
192.168.56.130 | UNREACHABLE! => {
    "changed": false, 
    "msg": "ERROR! SSH encountered an unknown error during the connection. We recommend you re-run the command using -vvvv, which will enable SSH debugging output to help diagnose the issue", 
    "unreachable": true
}
```
鍵認証にするみたい
http://qiita.com/HamaTech/items/21bb9761f326c4d4aa65

```
~ ❯❯❯ ansible -i hosts 192.168.56.130 -m ping                                                                                        ⏎
192.168.56.130 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```
