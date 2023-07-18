### Assume Role 설정

111111111111 계정 custodian-role에 포함된 policy

```
{
    "Version": "2012-10-17",
    "Statement": {
        "Effect": "Allow",
        "Action": "sts:AssumeRole",
        "Resource": [
            "arn:aws:iam::111111111111:role/lambda-function-deploy",
            "arn:aws:iam::222222222222:role/lambda-function-deploy",
            "arn:aws:iam::333333333333:role/lambda-function-deploy",
            "arn:aws:iam::444444444444:role/lambda-function-deploy"
        ]
    }
}
```

arn:aws:iam::222222222222:role/lambda-function-deploy을 이루는 policy에는 lambda를 만들 수 있는 권한을 가져야한다.

[Permissions] -> custodian 자체가 Lambda를 만드는 것
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "events:PutTargets",
                "events:DescribeRule",
                "iam:PassRole",
                "ec2:CreateTags",
                "events:PutRule",
                "lambda:*",
                "sts:*",
                "elasticloadbalancing:*",
                "events:ListTargetsByRule"
            ],
            "Resource": "*"
        }
    ]
}
```

[Trust relationships] -> 111111111111 계정에서 사용할 수 있어야 한다.
```

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::111111111111:root"
            },
            "Action": "sts:AssumeRole",
            "Condition": {}
        }
    ]
}
```
