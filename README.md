# AWS_notes


## IAM

### access policy , role , and policy
In the context of AWS, an IAM policy is a document that defines the permissions that are granted to a user, program, or role. These permissions specify what actions the principal is allowed to perform on specific AWS resources. For example, a policy might grant a user permission to read and write to an S3 bucket, or it might grant a program permission to invoke a specific Lambda function.

An access policy, on the other hand, is a policy that is attached to a specific resource, such as an S3 bucket or an SNS topic. This policy specifies which principals are allowed to access the resource and what actions they are allowed to perform on the resource.

In the case of the SNS topic access policy that you provided, the policy specifies that the AWS role with the ARN "arn:aws:iam::302250292538:role/rolelambda2" is allowed to perform the actions listed in the "Action" field. However, the access policy does not grant the role any permissions on its own. In order for the role to be able to actually perform these actions, it must have an attached IAM policy that grants it permission to do so.

For example, consider the following access policy for an SNS topic:

Copy code 

        {
        "Version": "2008-10-17",
        "Id": "__default_policy_ID",
        "Statement": [
            {
            "Sid": "__default_statement_ID",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::id:role/rolename"
            },
            "Action": [
                "SNS:Publish",
                "SNS:Subscribe"
            ],
            "Resource": "",
            "Condition": {
                "StringEquals": {
                "AWS:SourceOwner": "302250292538"
                }
            }
            }
        ]
        }
In this case, the access policy allows the AWS role with the ARN "arn:aws:iam::302250292538:role/rolelambda2" to publish messages to the SNS topic and to subscribe to the topic. However, in order for the role to actually be able to perform these actions, it must have an attached IAM policy that grants it permission to do so. For example, the role might have an attached policy like this:

Copy code

        {
        "Version": "2012-10-17",
        "Statement": [
            {
            "Effect": "Allow",
            "Action": [
                "SNS:Publish",
                "SNS:Subscribe"
            ],
            "Resource": "*"
            }
        ]
        }
This policy grants the role permission to perform the "SNS:Publish" and "SNS:Subscribe" actions on any SNS topic. With this policy attached to the role, the role will be able to publish messages to and subscribe to the SNS topic specified in the access policy.

In summary, an access policy specifies which principals are allowed to access a resource and what actions they are allowed to perform on the resource. However, in order for a principal to actually be able to perform these actions, it must have an attached IAM policy that grants it permission to do so.