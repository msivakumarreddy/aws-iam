# AWS IAM.

AWS IAM is almost same as general IAM. Components in IAM are.

* User
* Group
* Policy
* Role
    * IAM Roles have certain permissions defined for making AWS service requests.
    * IAM roles are not directly associated with a specific user or group.
    * They are intended to be assumable by anyone who needs them.
    * IAM role can be assumed by an AWS service, an application, or an authenticated user, granting them temporary security credentials to make AWS API calls