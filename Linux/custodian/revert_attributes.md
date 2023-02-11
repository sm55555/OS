## revert_attributes

#### [VPC]

```yaml
policies:
- name: revert-vpc-attribute
  resource: vpc
  mode:
    type: cloudtrail
    role: arn:aws:iam:111122223333:role/aws-temp-role
    events:
       - soruce: ec2.amazonaws.com
         event: ModifiyVpcAttribute
         ids: responseElements.vpcId
  filters:
     - type: value
       key: VpcId
       value: vpc-~~~~~
  actions:
    - type: auto-tag-user
      url: http://~~~~
      method: POST
```
