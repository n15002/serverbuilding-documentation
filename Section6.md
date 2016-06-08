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



