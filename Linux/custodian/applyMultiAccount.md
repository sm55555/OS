## 1. Assume Role 설정

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

## 2. Custodian 설정

```
c7n-org run -c accounts.yaml -s ./ -u ec2-create-terminate.yaml
```

#### accounts.yaml

accounts.yaml에 111111111111, 222222222222, 333333333333 에 custodian-role을 붙인 ec2-create-terminate.yaml을 만들어 준다.

```
accounts
  - account_id: '111111111111'
    name: one
    regions:
      - ap-northeast-2
    role: arn:aws:iam:111111111111:role/custodian-role
  - account_id: '222222222222'
    name: one
    regions:
      - ap-northeast-2
    role: arn:aws:iam:222222222222:role/custodian-role
  - account_id: '333333333333'
    name: one
    regions:
      - ap-northeast-2
    role: arn:aws:iam:13333333333:role/custodian-role
```

#### ec2-create-terminate.yaml

```
policies:
- name: ec2-create-terminate
  resource: ec2
  mode:
    type: cloudtrail
    role: arn:aws:iam:{account_id}:role/custodian-role
    events:
       - soruce: ec2.amazonaws.com
         event: RunInstances
         ids: "responseElements.instancesSet.items[].instanceId"
       - soruce: ec2.amazonaws.com
         event: TerminateInstances
         ids: "responseElements.instancesSet.items[].instanceId"
  filters:
     - tag:owner: absent 
  actions:
    - type: webhook
      tag: https://hooks......
      body: "message"
```

