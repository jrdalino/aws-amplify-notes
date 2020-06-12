# aws-amplify-notes

## Installation: Install Amplify CLI
```
$ npm install -g @aws-amplify/cli
$ amplify configure
```

```
$ environment % amplify configure
Scanning for plugins...
Plugin scan successful
Follow these steps to set up access to your AWS account:

Sign in to your AWS administrator account:
https://console.aws.amazon.com/
Press Enter to continue

Specify the AWS Region
? region:  ap-southeast-1
Specify the username of the new IAM user:
? user name:  jrdalino-amplify
Complete the user creation using the AWS console
https://console.aws.amazon.com/iam/home?region=undefined#/users$new?step=final&accessKey&userNames=jrdalino-amplify&permissionType=policies&policies=arn:aws:iam::aws:policy%2FAdministratorAccess
Press Enter to continue

Enter the access key of the newly created user:
? accessKeyId: ******
? secretAccessKey: ******
This would update/create the AWS Profile in your local machine
? Profile Name:  amplify

Successfully set up the new user.
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
? Select the environment setup: DEV (S3 only with HTTP)
? hosting bucket name myapp-20200418181729-hostingbucket
? index doc for the website index.html
? error doc for the website index.html

You can now publish your app using the following command:
Command: amplify publish
```
```
$ amplify status

Current Environment: dev

| Category | Resource name   | Operation | Provider plugin   |
| -------- | --------------- | --------- | ----------------- |
| Hosting  | S3AndCloudFront | Create    | awscloudformation |
| Auth     | myapp237c3585   | No Change | awscloudformation |
```

##  Step 4: Publish
```
$ amplify publish
✔ Successfully pulled backend environment dev from the cloud.

Current Environment: dev

| Category | Resource name   | Operation | Provider plugin   |
| -------- | --------------- | --------- | ----------------- |
| Hosting  | S3AndCloudFront | Create    | awscloudformation |
| Auth     | myapp237c3585   | No Change | awscloudformation |
? Are you sure you want to continue? Yes
⠙ Updating resources in the cloud. This may take a few minutes...

UPDATE_COMPLETE    authmyapp237c3585        AWS::CloudFormation::Stack Sat Apr 18 2020 18:19:19 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS hostingS3AndCloudFront   AWS::CloudFormation::Stack Sat Apr 18 2020 18:19:18 GMT+0800 (Singapore Standard Time) Resource creation Initiated
UPDATE_IN_PROGRESS authmyapp237c3585        AWS::CloudFormation::Stack Sat Apr 18 2020 18:19:17 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS hostingS3AndCloudFront   AWS::CloudFormation::Stack Sat Apr 18 2020 18:19:16 GMT+0800 (Singapore Standard Time)                            
UPDATE_IN_PROGRESS amplify-myapp-dev-174556 AWS::CloudFormation::Stack Sat Apr 18 2020 18:19:12 GMT+0800 (Singapore Standard Time) User Initiated             
⠙ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS S3Bucket                                                      AWS::S3::Bucket            Sat Apr 18 2020 18:19:23 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS S3Bucket                                                      AWS::S3::Bucket            Sat Apr 18 2020 18:19:21 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS amplify-myapp-dev-174556-hostingS3AndCloudFront-1N7Y6C8X6TKAM AWS::CloudFormation::Stack Sat Apr 18 2020 18:19:18 GMT+0800 (Singapore Standard Time) User Initiated             
⠧ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE S3Bucket AWS::S3::Bucket Sat Apr 18 2020 18:19:45 GMT+0800 (Singapore Standard Time) 
⠦ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE amplify-myapp-dev-174556-hostingS3AndCloudFront-1N7Y6C8X6TKAM AWS::CloudFormation::Stack Sat Apr 18 2020 18:19:47 GMT+0800 (Singapore Standard Time) 
⠇ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE hostingS3AndCloudFront AWS::CloudFormation::Stack Sat Apr 18 2020 18:19:52 GMT+0800 (Singapore Standard Time) 
⠹ Updating resources in the cloud. This may take a few minutes...

UPDATE_COMPLETE                     amplify-myapp-dev-174556 AWS::CloudFormation::Stack Sat Apr 18 2020 18:19:57 GMT+0800 (Singapore Standard Time) 
UPDATE_COMPLETE                     authmyapp237c3585        AWS::CloudFormation::Stack Sat Apr 18 2020 18:19:56 GMT+0800 (Singapore Standard Time) 
UPDATE_COMPLETE_CLEANUP_IN_PROGRESS amplify-myapp-dev-174556 AWS::CloudFormation::Stack Sat Apr 18 2020 18:19:55 GMT+0800 (Singapore Standard Time) 
✔ All resources are updated in the cloud

Hosting endpoint: http://myapp-20200418181729-hostingbucket-dev.s3-website-ap-southeast-2.amazonaws.com

yarn run v1.22.4
$ react-scripts build
Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

  131.83 KB  build/static/js/2.d552c88d.chunk.js
  3.63 KB    build/static/css/2.44a8782a.chunk.css
  920 B      build/static/js/main.c477d63f.chunk.js
  767 B      build/static/js/runtime-main.b1cc144f.js
  547 B      build/static/css/main.5f361e03.chunk.css

The project was built assuming it is hosted at /.
You can control this with the homepage field in your package.json.

The build folder is ready to be deployed.
You may serve it with a static server:

  yarn global add serve
  serve -s build

Find out more about deployment here:

  bit.ly/CRA-deploy

✨  Done in 40.71s.
frontend build command exited with code 0
✔ Uploaded files successfully.
Your app is published successfully.
http://myapp-20200418181729-hostingbucket-dev.s3-website-ap-southeast-2.amazonaws.com
```

## Cleanup
```
$ amplify remove hosting
$ amplify remove auth
$ amplify push
$ amplify delete
```

## References
- React Getting Started: https://aws-amplify.github.io/docs/js/react
- Authentication Getting Started: https://docs.amplify.aws/lib/auth/getting-started?platform=js
- Authentication: https://aws-amplify.github.io/docs/js/authentication

## Appendix: Adding Amplify Manually
- Step 1: Installation: Install Amplify CLI
```
$ npx create-react-app myapp2 && cd myapp2
```
- Step 2: Add Amplify and Amplify-React libraries to the ReactJS App
```
$ yarn add aws-amplify aws-amplify-react
```
- Step 3: Manually add /src/aws-exports
```
const awsmobile = {
    "aws_project_region": "ap-southeast-2"
};
export default awsmobile;
```
- Step 4: Edit ./src/App.js
```
...
import Amplify from 'aws-amplify';
import awsconfig from './aws-exports';
import { withAuthenticator } from 'aws-amplify-react';
import '@aws-amplify/ui/dist/style.css';
Amplify.configure(awsconfig);
...
export default withAuthenticator(App, true);
```
- Step 5: Test
```
$ yarn start
```
- Step 6: Re-use existing authentication resource as in https://docs.amplify.aws/lib/auth/start?platform=js#configure-your-application > Scroll to "Re-use existing authentication resource"
```
import Amplify, { Auth } from 'aws-amplify';
Amplify.configure({
    Auth: {
        // REQUIRED - Amazon Cognito Region
        region: 'ap-southeast-2',
        // OPTIONAL - Amazon Cognito User Pool ID
        userPoolId: ' ap-southeast-2_XGQmb0fKL',
        // OPTIONAL - Amazon Cognito Web Client ID (26-char alphanumeric string)
        userPoolWebClientId: '4imdhssvgm0s0h3em31brm14p2',
    }
});
// You can get the current config object
const currentConfig = Auth.configure();
```
- Step 7: Copy Sign Up, Sign in & Sign out code from https://docs.amplify.aws/lib/auth/emailpassword?platform=js
