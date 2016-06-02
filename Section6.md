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

