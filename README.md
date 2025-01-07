
# Others scenario
## Import AWS resources into CFN stacks
The resource import feature allows you to import existing AWS resources into a new or existing CloudFormation stack. This feature is useful if you want to start using CloudFormation to manage resources that were created outside of CloudFormation, without having to delete and recreate them, especially when the data in the resources cannot be delete, such as S3 bucket, Database and logs. 


### Only two items you need to provide during the import operation. 
- A template that describes the entire stack, including both the original stack resources and the resources you're importing. Each resource to import must have a DeletionPolicy attribute.

- Identifiers for the resources you're importing that CloudFormation can use to map the logical IDs in the template with the existing resources. For example, an AWS::S3::Bucket resource can be identified using its BucketName.

### Sample: Import a S3 bucekt into an existing CFN stack with one IAM role resource. `importBucket`
```yaml
Resources:
  SSMRole:
    Type: AWS::IAM::Role
    Properties:
      Description: Import
      AssumeRolePolicyDocument:
        Statement:
          - Effect: Allow
            Principal:
              Service:
                - ec2.amazonaws.com
            Action:
              - sts:AssumeRole
      ManagedPolicyArns:
        - arn:aws:iam::aws:policy/AmazonSSMManagedInstanceCore

  ImportS3Bucket:
    DeletionPolicy: Retain                 <<<<<<<
    Type: AWS::S3::Bucket
    Properties:
      BucketName: import-bucket-7
      # VersioningConfiguration:
      #   Status: Enabled
      # Tags:
      #   - Key: team
      #     Value: deployment   
```


------------
## Discover CloudFormation template samples. 
AWS provides various sample templates for customers to reference. When searching for examples, I suggest consulting the official documentation first, and consider using GitHub as a last resort. 

Testing the samples you find in Github before providng to cx. 

Here are the recommended resources:
- [AWS CloudFormation Templates](https://aws.amazon.com/cloudformation/resources/templates/)
- [AWS resource and property types reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html)
- [CloudFormation template snippets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-snippets.html)
  

### Sample: Defining ScheduleExpression Property of AWS::Scheduler::Schedule
- [Official documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-scheduler-schedule.html) ==> No example
- [Github](https://github.com/)
  
  Search item: 
  ```
  "AWS::Scheduler::Schedule" AND (path:*.yaml OR path:*.yml) AND "ScheduleExpression"
  ```

## Reference
1. [Import AWS resources into a CloudFormation stack with a resource import](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resource-import.html)
2. [Resource type support](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resource-import-supported-resources.html)
3. [A guide to discovering CloudFormation resource code samples](https://guide.aws.dev/articles/AR2E-mlj7sRzObQrBMrzB7Gg/a-guide-to-discovering-cloudformation-resource-code-samples) 



