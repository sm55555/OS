## Automatically tagging the resources

```yaml
policies:
- name: elastic-kubernetes-auto-tag
  resource: aws.eks
  comments: |
    Find EKS that has not been tagged with mandatory owner tag on-
    creation. Tag EKS with the user who  created it. This policy 
    does not apply on existing EKS.
  filters:
     - "tag:owner": absent 
  mode:
    type: cloudtrail
    events:
      - source: eks.amazonaws.com
        event: CreateCluster
        ids: requestParameters.name
    execution-options:
      output_dir: s3://s3bucket/cclogs/{account_id}/
    runtime: python3.8
  actions:
    - type: auto-tag-user
      tag: auto-owner
      principal_id_tag: principalid

```
