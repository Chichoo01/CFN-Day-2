Resource Attributes
---

Doc: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-product-attribute-reference.html

> Used to control on how we wish to handle Creation, Update and Deletion of specific resources.

CreationPolicy
--

- Supported resources: AWS::AutoScaling::AutoScalingGroup, AWS::EC2::Instance, and AWS::CloudFormation::WaitCondition
- Used during creation of these resources to prevent its status from reaching create complete until AWS CloudFormation receives a specified number of success signals or the timeout period is exceeded.
