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
