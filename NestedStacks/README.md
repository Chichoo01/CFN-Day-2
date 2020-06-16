Nested Stacks
---

Doc: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-nested-stacks.html

- Used to separate out these common components and create dedicated templates for them. 
- When AWS::CloudFormation::Stack is created as a resource within a stack, a nested stack is created.
- This helps overcome hard limit on the number of resources created per stack (200). 
- All updates to nested stack resources has to be done from parent stack.
- Updating child stack or resources directly would be considered as out-of-band change and might cause update failures on parent stack.

