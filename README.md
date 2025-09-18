# AWS-Migration
AWS migration templates for simulate regional migration project in the real-world scenario.
Follow below instruction to use the template:
- Save the repository in your local machine.
- Create the Stack in the AWS Hong Kong region (ap-east-1) using the AWS CLI or Console:
  
aws cloudformation create-stack \
  --stack-name migration-infra-main \
  --template-body file://nested-main-master-stack.yaml \
  --parameters \
    ParameterKey=EnvironmentName,ParameterValue=migration-prod \
    ParameterKey=KeyName,ParameterValue=MyHongKongKeyPairName \
    ParameterKey=DBMasterUserPassword,ParameterValue='TargetDBPassword123!' \
    ParameterKey=DBMasterUsername,ParameterValue=admin \
    ParameterKey=SourceDatabaseName,ParameterValue=my_singapore_database \
    ParameterKey=SourceServerName,ParameterValue=my-source-db.abc123.ap-southeast-1.rds.amazonaws.com \
    ParameterKey=SourceUsername,ParameterValue=source_db_user \
    ParameterKey=SourcePassword,ParameterValue='SourceDBPassword123!' \
  --capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM \
  --region ap-east-1 \
  --disable-rollback

- Monitor the stack creation in the CloudFormation console:

aws cloudformation describe-stacks \
  --stack-name migration-infra-main \
  --region ap-east-1 \
  --query 'Stacks[0].StackStatus'

- Check the events of the main stack:

aws cloudformation describe-stack-events \
  --stack-name migration-infra-main \
  --region ap-east-1 \
  --output table
