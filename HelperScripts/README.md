cfn-init:
---

* Fetch and parse metadata from AWS CloudFormation 
* Install packages 
* Write files to disk 
* Enable/disable and start/stop services

 - > Updating file in cfn-init creates a .bak file in the same directory.

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



