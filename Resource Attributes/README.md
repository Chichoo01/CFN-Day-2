Resource Attributes
---

Doc: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-product-attribute-reference.html

> Used to control on how we wish to handle Creation, Update and Deletion of specific resources.

CreationPolicy
--

- Used during creation of these resources to prevent its status from reaching create complete until AWS CloudFormation receives a specified number of success signals or the timeout period is exceeded.
- Supported resources: AWS::AutoScaling::AutoScalingGroup, AWS::EC2::Instance, and AWS::CloudFormation::WaitCondition

Syntax:

,,,
CreationPolicy:
  AutoScalingCreationPolicy:
    MinSuccessfulInstancesPercent: Integer
  ResourceSignal:    
    Count: Integer
    Timeout: String
,,,

UpdatePolicy
--

- Used to specify how AWS CloudFormation handles updates to certain resources.
- Supported resources:  AWS::AutoScaling::AutoScalingGroup, AWS::ElastiCache::ReplicationGroup, AWS::Elasticsearch::Domain, or AWS::Lambda::Alias

Available UpdatePolicy:

1) AutoScalingReplacingUpdate Policy

Creates a new ASG and replaces it with the old one once stabilized. 
,,,
UpdatePolicy:
  AutoScalingReplacingUpdate:
    WillReplace: Boolean
,,,

2) AutoScalingRollingUpdate Policy

Does rolling updates on the ASG

'''
UpdatePolicy:
  AutoScalingRollingUpdate:
    MaxBatchSize: Integer
    MinInstancesInService: Integer
    MinSuccessfulInstancesPercent: Integer
    PauseTime: String
    SuspendProcesses:
      - List of processes
    WaitOnResourceSignals: Boolean
'''

3) AutoScalingScheduledAction Policy

To specify how AWS CloudFormation handles updates for the MinSize, MaxSize, and DesiredCapacity properties when the AWS::AutoScaling::AutoScalingGroup resource has an associated scheduled action

Deletion Policy
--

Example:

'''
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  myS3Bucket:
    Type: AWS::S3::Bucket
    DeletionPolicy: Retain
'''

Options:

1) Delete
2) Retain
3) Snapshot

UpdateReplace Policy
--

To retain or (in some cases) backup the existing physical instance of a resource when it is replaced during a stack update operation. 


> Deletion Policy is used during a stack delete call and Update Replace Policy is used during stack update call.

DependsOn
--

When you add a DependsOn attribute to a resource, that resource is created only after the creation of the resource specified in the DependsOn attribute. 

Dependent stacks also have implicit dependencies. For example, if the properties of resource A use a !Ref to resource B, the following rule apply:

    Resource B is created before resource A.

    Resource A is deleted before resource B.


