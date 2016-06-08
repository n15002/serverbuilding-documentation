Section 6 AWS(Amazon Web Services)
=====

6-0 AWSコマンドラインインターフェイスのインストール
-----
http://aws.amazon.com/jp/cli/

```
~ ❯❯❯ aws configure
AWS Access Key ID [None]: ****************
AWS Secret Access Key [None]: **********************************
Default region name [None]: ap-northeast-1 
Default output format [None]: json
```

謎
```
~ ❯❯❯ aws ec2 describe-instances                                                                                        ⏎
A client error (UnauthorizedOperation) occurred when calling the DescribeInstances operation: You are not authorized to perform this operation.

~ ❯❯❯ aws iam list-policies                                                                                             ⏎
A client error (AccessDenied) occurred when calling the ListPolicies operation: User: arn:aws:iam::643182386713:user/n15001 is not authorized to perform: iam:ListPolicies on resource: policy path /
~ ❯❯❯       
```
アレな事してたからIPで弾かれてパスワード買えれなかった


コントロールパネルからEC2（AmazonLinux）を立ち上げる  
grusサーバに接続して、`ssh -i n15001.pem ec2-user@EC2のIP`でSSH接続が出来る事を確認する。

踏み台のやつやっとく
```
~ ❯❯❯ sudo vi .ssh/config 
Host grus
  User         n15001
  HostName     grusのIP
Host aws
  User ec2-user
  HostName    EC2のIP
  IdentityFile  ~/n15001.pem
  ProxyCommand ssh grus -W %h:%p
  
~ ❯❯❯ ssh aws
Password for n15001@grus:
Last login: Thu Jun  2 02:27:09 2016 from ******

       __|  __|_  )
       _|  (     /   Amazon Linux AMI
      ___|\___|___|
[ec2-user@ip-172-31-12-66 ~]$ 
```

```
[n15001@grus ~/ansible]$ ansible 54.238.210.10 -m ping -i hosts -u ec2-user --private-key ~/n15001.pem 
54.238.210.10 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```

6-3 S3
-----
```
[n15001@grus ~]$ aws configure
AWS Access Key ID [None]: ******************
AWS Secret Access Key [None]: **********************************
Default region name [None]: ap-northeast-1 #tokyo
Default output format [None]: json

[n15001@grus ~]$ aws ec2 describe-instances #色々情報見れるの確認する
[n15001@grus ~]$ aws s3 ls #s3バッケト一覧
[n15001@grus ~]$ aws s3 mb s3://n15001 #バケット作成 MakeBacket?
make_bucket: s3://n15001/
[n15001@grus ~]$ aws s3 ls #自分のバケットが作成されているか確認する
[n15001@grus ~]$ sudo vi index.html #公開用のHTML作成
[n15001@grus ~]$ aws s3 cp --acl public-read index.html s3://n15001/ #外部からの閲覧権限を与えながらアップロード
upload: ./index.html to s3://n15001/index.html
[n15001@grus ~]$ aws s3 ls s3://n15001
2016-06-08 09:43:17        109 index.html
```
`http://バケット名.s3-ap-northeast-1.amazonaws.com/ファイル名`でアクセスしてWebページが表示されれば成功
http://n15001.s3-ap-northeast-1.amazonaws.com/index.html

6-4 Cloudfront
-----
apachbenchを使って、cloudfrontでキャッシュさせる前とした後のWebサイト測定
AWSのサービスからCloudfrontを選択
Origin Domain Nameはドメインじゃないとダメみたい

```
[n15001@grus ~]$ ab -n 100 -c 100 http://ec2-54-199-207-38.ap-northeast-1.compute.amazonaws.com/wordpress/
This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking ec2-54-199-207-38.ap-northeast-1.compute.amazonaws.com (be patient).....done


Server Software:        nginx/1.8.1
Server Hostname:        ec2-54-199-207-38.ap-northeast-1.compute.amazonaws.com
Server Port:            80

Document Path:          /wordpress/
Document Length:        65284 bytes

Concurrency Level:      100
Time taken for tests:   35.463 seconds
Complete requests:      100
Failed requests:        75
   (Connect: 0, Receive: 0, Length: 75, Exceptions: 0)
Non-2xx responses:      64
Total transferred:      2350489 bytes
HTML transferred:       2323089 bytes
Requests per second:    2.82 [#/sec] (mean)
Time per request:       35462.665 [ms] (mean)
Time per request:       354.627 [ms] (mean, across all concurrent requests)
Transfer rate:          64.73 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       37   82  12.5     86      88
Processing:  1223 12585 6777.0  12838   35374
Waiting:     1032 11386 5258.2  12724   20363
Total:       1305 12667 6776.9  12925   35459

Percentage of the requests served within a certain time (ms)
  50%  12925
  66%  14976
  75%  15113
  80%  15297
  90%  18938
  95%  20450
  98%  35459
  99%  35459
 100%  35459 (longest request)

```



Edit Geo-Restrictions
Enable Geo-Restriction →Yes
Restriction Type → WhiteList
JPを追加する

USインスタンスを立ち上げてWebサイトにアクセスしてみる
![Cloudfrontの地域のアレ](https://raw.githubusercontent.com/n15001/serverbuilding-documentation/master/Screenshot%20from%202016-06-08%2018-24-42.png 'are')
