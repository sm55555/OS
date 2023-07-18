
```
policies:
- name: ec2-create-terminate
  resource: ec2
  mode:
    type: cloudtrail
    role: arn:aws:iam:111122223333:role/custodian-role
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
