## Automatically tagging the resources

1. First You have to make policy as shonw in the document below.
2. and Run command

Use "$ custodian run --dryrun" command to check the affected resource and it does not run any actions on the resources.

```
custodian run --dryrun -c example.yml -s out
```

Use "$ custodian run" command to deploy the policy to your cloud account.

```
custodian run --output-dir=[anywhere] example.yml
```



#### [EC2]

```yaml
policies:
- name: ec2-auto-tag
  resource: aws.ec2
  mode:
    type: cloudtrail
    role: arn:aws:iam:~~
    events:
       - RunInstances
  filters:
     - "tag:owner": absent 
  actions:
    - type: auto-tag-user
      tag: owner
    - type : tag
      tags:
        CreationDate: "{now:%Y%m%d}"
        other : aaa
```
