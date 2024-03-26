# IAM Role

* IAM Roles have certain permissions defined for making AWS service requests.
* IAM roles are not directly associated with a specific user or group.
* They are intended to be assumable by anyone who needs them.
* IAM role can be assumed by an AWS service, an application, or an authenticated user, granting them temporary security credentials to make AWS API calls.

Our AMI Details
* Name: devops-practice
* username: centos
* password: DevOps321
* Security Group: create a SG that allows port 22 at least to connect.

# Use case-1
* Create a role for EC2
* List All buckets
* List objects inside a specific bucket.

# Use case-2
* Create a role for EC2
* It can create EC2 instances.
* It can create/update records in Route53.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:RunInstances",
                "ec2:DescribeInstances",
                "ec2:CreateTags"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "route53:ChangeResourceRecordSets",
                "route53:ListHostedZones",
                "route53:GetHostedZone",
                "route53:ListResourceRecordSets"
            ],
            "Resource": "*"
        }
    ]
}
```