## Automatically tagging the resources


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
