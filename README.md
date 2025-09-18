# AWS-Migration
AWS migration templates for simulate regional migration project in the real-world scenario.
Follow below instruction to use the template:
- Save the repository in your local machine.
- Create the Stack in the AWS Hong Kong region (ap-east-1) using the AWS CLI or Console:
  
  aws cloudformation create-stack \
  --stack-name migration-infrastructure \
  --template-body file://migration-setup.yaml \
  --parameters ParameterKey=KeyName,ParameterValue=YourKeyName \
  --region ap-east-1

- Monitor the stack creation in the CloudFormation console.
