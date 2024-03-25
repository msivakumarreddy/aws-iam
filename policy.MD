# AWS IAM Policy

IAM policy is basically a JSON document that controls what actions we can perform on which resources, under what conditions.

### identity based policy
If a policy is attached to IAM user, group or IAM Role, then it is called as identity based policy.

Below policy can grant all actions on EC2 resources in us-east-1 region

```
{
    "Version": "2012-10-17",
    "Statement": [ 
        {
            "Effect": "Allow", 
            "Action": "ec2:*", 
            "Resource": "*", 
            "Condition": { 
                "StringEquals": {
                    "ec2:Region": "us-east-1"
                }
            }
        }
    ]
}
```

### Resource based policy
If a policy is attached to resource like S3, DynamoDB, etc. are called resource based policy.
**NOTE:** There is an extra item **Principal** for resource based policy apart from identity based policy.

Refer below documentation to check the services supported by Resource based policy
https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowUserToListBucket",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::account-id:user/joindevops"
      },
      "Action": [
        "s3:ListBucket"
      ],
      "Resource": "arn:aws:s3:::your-bucket-name"
    },
    {
      "Sid": "AllowUserToListObjects",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::account-id:user/joindevops"
      },
      "Action": [
        "s3:GetObject"
      ],
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}

```

### inline policy
* Inline policies have a direct, one-to-one relationship with a single IAM entity, which can be an IAM user, group, or role. 
* This means that an inline policy is created specifically for and attached directly to one IAM entity. 
* When a entity is deleted inline policy is also deleted.
* Typically used for very specific permissions that should not be reusable.

### Managed policies
Managed policies can be attached to User, Groups and Roles.
* AWS Managed policy
    * Created and managed by AWS.
    * We can't edit or delete these policies.
* Custom managed policy
    * Created and managed by us.
    * We can edit or delete them.

### Attribute based policy

We can attach this policy to DBAdmin team which is handling Production DB.
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                    "rds:DescribeDBInstances",
                    "rds:DescribeDBClusters",
                    "rds:DescribeGlobalClusters"
            ],
            "Resource": "*"
        },
        
        {
            "Effect": "Allow",
            "Action": [
                "rds:RebootDBInstance",
                "rds:StartDBInstance",
                "rds:StopDBInstance"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalTag/Team": "DBAdmins",
                    "rds:db-tag/Environment": "prod"
                }
            }
        }
    ]
}
```

We can attach this policy to Development team which is handling Development DB.
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                    "rds:DescribeDBInstances",
                    "rds:DescribeDBClusters",
                    "rds:DescribeGlobalClusters"
            ],
            "Resource": "*"
        },
        
        {
            "Effect": "Allow",
            "Action": [
                "rds:RebootDBInstance",
                "rds:StartDBInstance",
                "rds:StopDBInstance"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalTag/Team": "Development",
                    "rds:db-tag/Environment": "dev"
                }
            }
        }
    ]
}
```



