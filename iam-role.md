Here's how you can create a new IAM role in the AWS Management Console:

1. Open the IAM console at https://console.aws.amazon.com/iam/.
2. In the navigation pane, choose Roles, and then choose Create role.
3. Under Select type of trusted entity, choose AWS service.
4. Under Choose the service that will use this role, choose Lambda.
5. Choose Next: Permissions.
6. In the Attach permissions policies page, choose the policies that grant the necessary permissions. For a Lambda function, you might start with the AWSLambdaBasicExecutionRole policy, which grants the permissions that a function needs to write logs to CloudWatch Logs.
7. Choose Next: Tags.
8. (Optional) Add metadata to the role by attaching tags as key-value pairs. For more information about using tags in IAM, see Tagging IAM entities in the IAM User Guide.
9. Choose Next: Review.
10. For Role name, enter a name for the role, such as lambda_execution_role.
11. Review the role and then choose Create role.

After you create the role, you can find its ARN in the role's summary page. The ARN is the role's unique identifier and looks something like this: arn:aws:iam::123456789012:role/lambda_execution_role. This is the value you would use for the role field in your Lambda function's deploy configuration.