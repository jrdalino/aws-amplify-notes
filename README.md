# aws-amplify-notes

## Installation: Install Amplify CLI
```
$ npm install -g @aws-amplify/cli
$ amplify configure
```

## Step 1: Create a new app, initialize and install Amplify. The following resources will be created
- Amplify Project: myapp
- Cloudformation Stack: amplify-myapp-dev-174556
- S3 Bucket: amplify-myapp-dev-174556-deployment
- IAM Role: amplify-myapp-dev-174556-authRole
- IAM Role: amplify-myapp-dev-174556-unauthRole
```
$ npx create-react-app myapp && cd myapp
$ amplify init
Note: It is recommended to run this command from the root of your app directory
? Enter a name for the project myapp
? Enter a name for the environment dev
? Choose your default editor: Visual Studio Code
? Choose the type of app that you're building javascript
Please tell us about your project
? What javascript framework are you using react
? Source Directory Path:  src
? Distribution Directory Path: build
? Build Command:  yarn build
? Start Command: yarn start
Using default provider  awscloudformation

For more information on AWS Profiles, see:
https://docs.aws.amazon.com/cli/latest/userguide/cli-multiple-profiles.html

? Do you want to use an AWS profile? Yes
? Please choose the profile you want to use default
Adding backend environment dev to AWS Amplify Console app: d1yi793gb9i9me
⠧ Initializing project in the cloud...

CREATE_IN_PROGRESS DeploymentBucket         AWS::S3::Bucket            Sat Apr 18 2020 17:46:06 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UnauthRole               AWS::IAM::Role             Sat Apr 18 2020 17:46:06 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS AuthRole                 AWS::IAM::Role             Sat Apr 18 2020 17:46:05 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UnauthRole               AWS::IAM::Role             Sat Apr 18 2020 17:46:05 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS AuthRole                 AWS::IAM::Role             Sat Apr 18 2020 17:46:05 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS DeploymentBucket         AWS::S3::Bucket            Sat Apr 18 2020 17:46:04 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS amplify-myapp-dev-174556 AWS::CloudFormation::Stack Sat Apr 18 2020 17:46:01 GMT+0800 (Singapore Standard Time) User Initiated             
⠹ Initializing project in the cloud...

CREATE_COMPLETE AuthRole AWS::IAM::Role Sat Apr 18 2020 17:46:20 GMT+0800 (Singapore Standard Time) 
⠋ Initializing project in the cloud...

CREATE_COMPLETE UnauthRole AWS::IAM::Role Sat Apr 18 2020 17:46:21 GMT+0800 (Singapore Standard Time) 
⠙ Initializing project in the cloud...

CREATE_COMPLETE DeploymentBucket AWS::S3::Bucket Sat Apr 18 2020 17:46:27 GMT+0800 (Singapore Standard Time) 
⠙ Initializing project in the cloud...

CREATE_COMPLETE amplify-myapp-dev-174556 AWS::CloudFormation::Stack Sat Apr 18 2020 17:46:31 GMT+0800 (Singapore Standard Time) 
✔ Successfully created initial AWS cloud resources for deployments.
✔ Initialized provider successfully.
Initialized your environment successfully.

Your project has been successfully initialized and connected to the cloud!

Some next steps:
"amplify status" will show you what you've added already and if it's locally configured or deployed
"amplify add <category>" will allow you to add features like user login or a backend API
"amplify push" will build all your local backend resources and provision it in the cloud
“amplify console” to open the Amplify Console and view your project status
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud

Pro tip:
Try "amplify add api" to create a backend API and then "amplify publish" to deploy everything
```
```
$ yarn start
```

## Step 2: Add Auth, provision auth resources in the cloud
```
$ amplify add auth
Using service: Cognito, provided by: awscloudformation
 
 The current configured provider is Amazon Cognito. 
 
 Do you want to use the default authentication and security configuration? Default configuration
 Warning: you will not be able to edit these selections. 
 How do you want users to be able to sign in? Email
 Do you want to configure advanced settings? No, I am done.
Successfully added resource myapp237c3585 locally

Some next steps:
"amplify push" will build all your local backend resources and provision it in the cloud
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud
```
- Push local backend resources to the cloud
```
$ amplify push
✔ Successfully pulled backend environment dev from the cloud.

Current Environment: dev

| Category | Resource name | Operation | Provider plugin   |
| -------- | ------------- | --------- | ----------------- |
| Auth     | myapp237c3585 | Create    | awscloudformation |
? Are you sure you want to continue? Yes
⠹ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UpdateRolesWithIDPFunctionRole AWS::IAM::Role             Sat Apr 18 2020 18:02:26 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS authmyapp237c3585              AWS::CloudFormation::Stack Sat Apr 18 2020 18:02:25 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UpdateRolesWithIDPFunctionRole AWS::IAM::Role             Sat Apr 18 2020 18:02:25 GMT+0800 (Singapore Standard Time)                            
UPDATE_IN_PROGRESS amplify-myapp-dev-174556       AWS::CloudFormation::Stack Sat Apr 18 2020 18:02:19 GMT+0800 (Singapore Standard Time) User Initiated             
⠹ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS authmyapp237c3585 AWS::CloudFormation::Stack Sat Apr 18 2020 18:02:26 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠇ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS SNSRole                                                  AWS::IAM::Role             Sat Apr 18 2020 18:02:33 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS SNSRole                                                  AWS::IAM::Role             Sat Apr 18 2020 18:02:32 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS amplify-myapp-dev-174556-authmyapp237c3585-1M93DB0IO1FGT AWS::CloudFormation::Stack Sat Apr 18 2020 18:02:26 GMT+0800 (Singapore Standard Time) User Initiated             
⠸ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE UpdateRolesWithIDPFunctionRole AWS::IAM::Role Sat Apr 18 2020 18:02:42 GMT+0800 (Singapore Standard Time) 
⠦ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE SNSRole AWS::IAM::Role Sat Apr 18 2020 18:02:49 GMT+0800 (Singapore Standard Time) 
⠏ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPool AWS::Cognito::UserPool Sat Apr 18 2020 18:02:53 GMT+0800 (Singapore Standard Time) 
⠋ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    UserPool AWS::Cognito::UserPool Sat Apr 18 2020 18:02:55 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UserPool AWS::Cognito::UserPool Sat Apr 18 2020 18:02:55 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠙ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    UserPoolClientWeb AWS::Cognito::UserPoolClient Sat Apr 18 2020 18:03:01 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UserPoolClientWeb AWS::Cognito::UserPoolClient Sat Apr 18 2020 18:03:01 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_COMPLETE    UserPoolClient    AWS::Cognito::UserPoolClient Sat Apr 18 2020 18:03:00 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UserPoolClient    AWS::Cognito::UserPoolClient Sat Apr 18 2020 18:03:00 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UserPoolClientWeb AWS::Cognito::UserPoolClient Sat Apr 18 2020 18:02:59 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UserPoolClient    AWS::Cognito::UserPoolClient Sat Apr 18 2020 18:02:58 GMT+0800 (Singapore Standard Time)                            
⠴ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPoolClientRole AWS::IAM::Role Sat Apr 18 2020 18:03:04 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UserPoolClientRole AWS::IAM::Role Sat Apr 18 2020 18:03:04 GMT+0800 (Singapore Standard Time)                            
⠼ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    UserPoolClientLambda AWS::Lambda::Function Sat Apr 18 2020 18:03:24 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UserPoolClientLambda AWS::Lambda::Function Sat Apr 18 2020 18:03:24 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UserPoolClientLambda AWS::Lambda::Function Sat Apr 18 2020 18:03:23 GMT+0800 (Singapore Standard Time)                            
CREATE_COMPLETE    UserPoolClientRole   AWS::IAM::Role        Sat Apr 18 2020 18:03:20 GMT+0800 (Singapore Standard Time)                            
⠋ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPoolClientLambdaPolicy AWS::IAM::Policy Sat Apr 18 2020 18:03:29 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UserPoolClientLambdaPolicy AWS::IAM::Policy Sat Apr 18 2020 18:03:27 GMT+0800 (Singapore Standard Time)                            
⠼ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPoolClientLogPolicy    AWS::IAM::Policy Sat Apr 18 2020 18:03:46 GMT+0800 (Singapore Standard Time) 
CREATE_COMPLETE    UserPoolClientLambdaPolicy AWS::IAM::Policy Sat Apr 18 2020 18:03:43 GMT+0800 (Singapore Standard Time) 
⠼ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPoolClientLogPolicy AWS::IAM::Policy Sat Apr 18 2020 18:03:48 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠼ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE UserPoolClientLogPolicy AWS::IAM::Policy Sat Apr 18 2020 18:04:02 GMT+0800 (Singapore Standard Time) 
⠦ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPoolClientInputs Custom::LambdaCallout Sat Apr 18 2020 18:04:05 GMT+0800 (Singapore Standard Time) 
⠧ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    UserPoolClientInputs Custom::LambdaCallout Sat Apr 18 2020 18:04:09 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UserPoolClientInputs Custom::LambdaCallout Sat Apr 18 2020 18:04:09 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠹ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS IdentityPool AWS::Cognito::IdentityPool Sat Apr 18 2020 18:04:12 GMT+0800 (Singapore Standard Time) 
⠸ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS IdentityPool AWS::Cognito::IdentityPool Sat Apr 18 2020 18:04:14 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠇ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    IdentityPoolRoleMap AWS::Cognito::IdentityPoolRoleAttachment Sat Apr 18 2020 18:04:20 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS IdentityPoolRoleMap AWS::Cognito::IdentityPoolRoleAttachment Sat Apr 18 2020 18:04:20 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS IdentityPoolRoleMap AWS::Cognito::IdentityPoolRoleAttachment Sat Apr 18 2020 18:04:18 GMT+0800 (Singapore Standard Time)                            
CREATE_COMPLETE    IdentityPool        AWS::Cognito::IdentityPool               Sat Apr 18 2020 18:04:15 GMT+0800 (Singapore Standard Time)                            
⠹ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE amplify-myapp-dev-174556-authmyapp237c3585-1M93DB0IO1FGT AWS::CloudFormation::Stack Sat Apr 18 2020 18:04:22 GMT+0800 (Singapore Standard Time) 
⠴ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UpdateRolesWithIDPFunction AWS::Lambda::Function      Sat Apr 18 2020 18:04:45 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UpdateRolesWithIDPFunction AWS::Lambda::Function      Sat Apr 18 2020 18:04:44 GMT+0800 (Singapore Standard Time)                            
CREATE_COMPLETE    authmyapp237c3585          AWS::CloudFormation::Stack Sat Apr 18 2020 18:04:42 GMT+0800 (Singapore Standard Time)                            
⠦ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE UpdateRolesWithIDPFunction AWS::Lambda::Function Sat Apr 18 2020 18:04:45 GMT+0800 (Singapore Standard Time) 
⠏ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UpdateRolesWithIDPFunctionOutputs Custom::LambdaCallout Sat Apr 18 2020 18:04:47 GMT+0800 (Singapore Standard Time) 
⠧ Updating resources in the cloud. This may take a few minutes...

UPDATE_COMPLETE_CLEANUP_IN_PROGRESS amplify-myapp-dev-174556          AWS::CloudFormation::Stack Sat Apr 18 2020 18:04:55 GMT+0800 (Singapore Standard Time)                            
CREATE_COMPLETE                     UpdateRolesWithIDPFunctionOutputs Custom::LambdaCallout      Sat Apr 18 2020 18:04:52 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS                  UpdateRolesWithIDPFunctionOutputs Custom::LambdaCallout      Sat Apr 18 2020 18:04:52 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠼ Updating resources in the cloud. This may take a few minutes...

UPDATE_COMPLETE amplify-myapp-dev-174556 AWS::CloudFormation::Stack Sat Apr 18 2020 18:04:56 GMT+0800 (Singapore Standard Time) 
✔ All resources are updated in the cloud
```
- Add Amplify and Amplify-React libraries to the ReactJS App
```
$ yarn add aws-amplify aws-amplify-react
```
- Edit ./src/App.js
```
...
import Amplify from 'aws-amplify';
import awsconfig from './aws-exports';
import { withAuthenticator } from 'aws-amplify-react'; // or 'aws-amplify-react-native';
import '@aws-amplify/ui/dist/style.css';

Amplify.configure(awsconfig);

...

export default withAuthenticator(App, true);
```
```
$ yarn start
```


## Step 3: Add Hosting
```
$ amplify add hosting (DEV)
$ amplify status
$ amplify update hosting (PROD) 
```

##  Step 4: Publish
```
$ amplify publish
```

## References
- React Getting Started: https://aws-amplify.github.io/docs/js/react
- Authentication Getting Started: https://docs.amplify.aws/lib/auth/getting-started?platform=js
- Authentication: https://aws-amplify.github.io/docs/js/authentication
