cfn-init:
---

* Fetch and parse metadata from AWS CloudFormation 
* Install packages 
* Write files to disk 
* Enable/disable and start/stop services

> Updating file in cfn-init creates a .bak file in the same directory.

Doesn’t not need credentials. It checks for stack membership and limits the scope of the call to the stack that the instance belongs to. 

Syntax:

'''
cfn-init --stack|-s stack.name.or.id \
         --resource|-r logical.resource.id \
         --region region
         --access-key access.key \
         --secret-key secret.key \
         --role rolename\
         --credential-file|-f credential.file \
         --configsets|-c config.sets \
         --url|-u service.url \
         --http-proxy HTTP.proxy \
         --https-proxy HTTPS.proxy \
         --verbose|-v

,,,

AWS::CloudFormation::Init Metadata structure: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-init.html

AWS::CloudFormation::Authentication Metadata structure: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-authentication.html

— Used to include authentication information for a file or source that you specify with AWS::CloudFormation::Init

cfn-signal:
---

The cfn-signal helper script signals AWS CloudFormation to indicate whether Amazon EC2 instances have been successfully created or updated. If you install and configure software applications on instances, you can signal AWS CloudFormation when those software applications are ready. 

use the cfn-signal script in conjunction with a CreationPolicy or an Auto Scaling group with a WaitOnResourceSignals update policy

Syntax:

'''
cfn-signal --success|-s signal.to.send \
        --access-key access.key \
        --credential-file|-f credential.file \
        --exit-code|-e exit.code \
        --http-proxy HTTP.proxy \
        --https-proxy HTTPS.proxy \
        --id|-i unique.id \
        --region AWS.region \
        --resource resource.logical.ID \
        --role IAM.role.name \
        --secret-key secret.key \
        --stack stack.name.or.stack.ID \
        --url AWS CloudFormation.endpoint
'''


> Another way to signal back to CFN is using WaitCondition with WaitConditionHandle.

You can use a wait condition for situations like the following:

    To coordinate stack resource creation with configuration actions that are external to the stack creation

    To track the status of a configuration process

WaitConditionHandle creates a pre-signed S3 URL which the service polls to to get response signal abck from the stack resource.

SignalResource API
--
Sends a signal to the specified resource with a success or failure status. You can use the SignalResource API in conjunction with a creation policy or update policy. AWS CloudFormation doesn't proceed with a stack creation or update until resources receive the required number of signals or the timeout period is exceeded. The SignalResource API is useful in cases where you want to send signals from anywhere other than an Amazon EC2 instance. 

Example: aws cloudformation signal-resource --stack-name ec2helperscript --logical-resource-id Instance --status SUCCESS --unique-id i-01a87d55951bc6ab0

cfn-hup:
---

The cfn-hup helper is a daemon that detects changes in resource metadata and runs user-specified actions when a change is detected. This allows you to make configuration updates on your running Amazon EC2 instances through the UpdateStack API action. 

cfn-hup.conf -> stores the name of the stack and the AWS credentials that the cfn-hup daemon targets.

'''
[main]
stack=<stack-name-or-id>  
'''

On Windows, the default path is system_drive\cfn. On Linux, the default path is /etc/cfn. 
 
hooks.conf -> The user actions that the cfn-hup daemon calls periodically are defined in the hooks.conf configuration file.

'''
[hookname]
triggers=post.add or post.update or post.remove
path=Resources.<logicalResourceId> (.Metadata or .PhysicalResourceId)(.<optionalMetadatapath>)
action=<arbitrary shell command>
runas=<runas user> 
'''

hooks.d Directory -> contains the hooks.conf files. Location: /etc/cfn/



