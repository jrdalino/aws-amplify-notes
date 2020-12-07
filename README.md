# aws-amplify-notes

## What problem does AWS Amplify solve?
- I want to build, launch a new mobile or web product to test my hypothesis. It currently takes X days to do this, I want to do it in Y days. 

## How does AWS Amplify solve this?
Faster App Dev of mobile or web MVP’s through:
### AWS Framework https://aws.amazon.com/amplify/framework/
- Amplify Libraries: https://docs.amplify.aws/lib/q/platform/js
- CLI (Toolchain) https://docs.amplify.aws/cli
- UI Styling: https://aws-amplify.github.io/media/ui_library (Colors, Typography, Components)
### AWS Amplify Console: https://ap-southeast-1.console.aws.amazon.com/amplify/home?region=ap-southeast-1#/

## What alternatives are available?
### AWS Amplify
- Full-stack: Web + Mobile + Backend
- https://aws.amazon.com/amplify/framework/
### AWS Serverless Application Model: 
- Used for backend, not for front end
- https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html
### Serverless Framework: 
- Supports Multi-cloud
- https://www.serverless.com/framework/docs/providers/aws/guide/intro

## Prerequisites
- Install Amplify CLI and Configure
```
$ npm install -g @aws-amplify/cli
$ amplify configure --usage-data-off
$ amplify configure
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
## Demo
### Step 1: Create a new react app
```
$ npx create-react-app myproject-amplify-demo && cd myproject-amplify-demo
...
Success! Created myproject-amplify-demo at /Users/jrdalino/environment/myproject-amplify-demo
Inside that directory, you can run several commands:

  yarn start
    Starts the development server.

  yarn build
    Bundles the app into static files for production.

  yarn test
    Starts the test runner.

  yarn eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd myproject-amplify-demo
  yarn start

Happy hacking!
```

### Step 2: Initialize AWS Amplify. 
- Run this command
```
$ amplify init
Note: It is recommended to run this command from the root of your app directory
? Enter a name for the project myprojectamplifydemo
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
https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html

? Do you want to use an AWS profile? Yes
? Please choose the profile you want to use amplify
Adding backend environment dev to AWS Amplify Console app: d3k4wgamyjs0uh
⠴ Initializing project in the cloud...

CREATE_IN_PROGRESS AuthRole                                AWS::IAM::Role             Fri Dec 04 2020 17:24:25 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UnauthRole                              AWS::IAM::Role             Fri Dec 04 2020 17:24:25 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UnauthRole                              AWS::IAM::Role             Fri Dec 04 2020 17:24:24 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS AuthRole                                AWS::IAM::Role             Fri Dec 04 2020 17:24:24 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS DeploymentBucket                        AWS::S3::Bucket            Fri Dec 04 2020 17:24:23 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS amplify-myprojectamplifydemo-dev-172354 AWS::CloudFormation::Stack Fri Dec 04 2020 17:24:19 GMT+0800 (Singapore Standard Time) User Initiated             
⠼ Initializing project in the cloud...

CREATE_IN_PROGRESS DeploymentBucket AWS::S3::Bucket Fri Dec 04 2020 17:24:25 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠦ Initializing project in the cloud...

CREATE_COMPLETE UnauthRole AWS::IAM::Role Fri Dec 04 2020 17:24:45 GMT+0800 (Singapore Standard Time) 
⠇ Initializing project in the cloud...

CREATE_COMPLETE AuthRole AWS::IAM::Role Fri Dec 04 2020 17:24:45 GMT+0800 (Singapore Standard Time) 
⠇ Initializing project in the cloud...

CREATE_COMPLETE amplify-myprojectamplifydemo-dev-172354 AWS::CloudFormation::Stack Fri Dec 04 2020 17:24:49 GMT+0800 (Singapore Standard Time) 
CREATE_COMPLETE DeploymentBucket                        AWS::S3::Bucket            Fri Dec 04 2020 17:24:46 GMT+0800 (Singapore Standard Time) 
✔ Successfully created initial AWS cloud resources for deployments.
✔ Initialized provider successfully.
Initialized your environment successfully.

Your project has been successfully initialized and connected to the cloud!

Some next steps:
"amplify status" will show you what you've added already and if it's locally configured or deployed
"amplify add <category>" will allow you to add features like user login or a backend API
"amplify push" will build all your local backend resources and provision it in the cloud
"amplify console" to open the Amplify Console and view your project status
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud

Pro tip:
Try "amplify add api" to create a backend API and then "amplify publish" to deploy everything
```
- This will create the following AWS Resources:
```
- Amplify Project: myprojectamplifydemo
- Cloudformation Stack: amplify-myprojectamplifydemo-dev-172354
- S3 Bucket: amplify-myprojectamplifydemo-dev-172354-deployment
- IAM Role: amplify-myprojectamplifydemo-dev-172354-authRole
- IAM Role: amplify-myprojectamplifydemo-dev-172354-unauthRole
```
- This create the following resources
```
$ pwd
/Users/jrdalino/environment/myproject-amplify-demo/amplify
$ ls
#current-cloud-backend	backend			cli.json		team-provider-info.json
$ pwd
/Users/jrdalino/environment/myproject-amplify-demo/src
$ cat aws-exports.js 
/* eslint-disable */
// WARNING: DO NOT EDIT. This file is automatically generated by AWS Amplify. It will be overwritten.

const awsmobile = {
    "aws_project_region": "ap-southeast-1"
};
$ cat .gitignore
...

#amplify
amplify/\#current-cloud-backend
amplify/.config/local-*
amplify/mock-data
...
```

### Step 3: Add Auth, provision auth resources in the cloud
```
$ amplify add auth    
Using service: Cognito, provided by: awscloudformation
 
 The current configured provider is Amazon Cognito. 
 
 Do you want to use the default authentication and security configuration? Default configuration
 Warning: you will not be able to edit these selections. 
 How do you want users to be able to sign in? Email
 Do you want to configure advanced settings? No, I am done.
Successfully added auth resource myprojectamplifydemo5a4834e7 locally

Some next steps:
"amplify push" will build all your local backend resources and provision it in the cloud
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud
```

### Step 4: Push local backend resources to the cloud
```
$ amplify push 
✔ Successfully pulled backend environment dev from the cloud.

Current Environment: dev

| Category | Resource name                | Operation | Provider plugin   |
| -------- | ---------------------------- | --------- | ----------------- |
| Auth     | myprojectamplifydemo5a4834e7 | Create    | awscloudformation |
? Are you sure you want to continue? Yes
⠸ Updating resources in the cloud. This may take a few minutes...

UPDATE_IN_PROGRESS DeploymentBucket                        AWS::S3::Bucket            Mon Dec 07 2020 14:42:55 GMT+0800 (Singapore Standard Time)               
UPDATE_IN_PROGRESS UnauthRole                              AWS::IAM::Role             Mon Dec 07 2020 14:42:55 GMT+0800 (Singapore Standard Time)               
UPDATE_IN_PROGRESS AuthRole                                AWS::IAM::Role             Mon Dec 07 2020 14:42:54 GMT+0800 (Singapore Standard Time)               
UPDATE_IN_PROGRESS amplify-myprojectamplifydemo-dev-172354 AWS::CloudFormation::Stack Mon Dec 07 2020 14:42:50 GMT+0800 (Singapore Standard Time) User Initiated
⠴ Updating resources in the cloud. This may take a few minutes...

UPDATE_COMPLETE UnauthRole AWS::IAM::Role Mon Dec 07 2020 14:43:13 GMT+0800 (Singapore Standard Time) 
UPDATE_COMPLETE AuthRole   AWS::IAM::Role Mon Dec 07 2020 14:43:13 GMT+0800 (Singapore Standard Time) 
⠧ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS authmyprojectamplifydemo5a4834e7 AWS::CloudFormation::Stack Mon Dec 07 2020 14:43:18 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UpdateRolesWithIDPFunctionRole   AWS::IAM::Role             Mon Dec 07 2020 14:43:17 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS authmyprojectamplifydemo5a4834e7 AWS::CloudFormation::Stack Mon Dec 07 2020 14:43:17 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UpdateRolesWithIDPFunctionRole   AWS::IAM::Role             Mon Dec 07 2020 14:43:16 GMT+0800 (Singapore Standard Time)                            
UPDATE_COMPLETE    DeploymentBucket                 AWS::S3::Bucket            Mon Dec 07 2020 14:43:15 GMT+0800 (Singapore Standard Time)                            
⠏ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS amplify-myprojectamplifydemo-dev-172354-authmyprojectamplifydemo5a4834e7-Y8FLQDMPUIO8 AWS::CloudFormation::Stack Mon Dec 07 2020 14:43:17 GMT+0800 (Singapore Standard Time) User Initiated
⠧ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS SNSRole AWS::IAM::Role Mon Dec 07 2020 14:43:25 GMT+0800 (Singapore Standard Time) 
⠧ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS SNSRole AWS::IAM::Role Mon Dec 07 2020 14:43:26 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠦ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE UpdateRolesWithIDPFunctionRole AWS::IAM::Role Mon Dec 07 2020 14:43:38 GMT+0800 (Singapore Standard Time) 
⠏ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE SNSRole AWS::IAM::Role Mon Dec 07 2020 14:43:46 GMT+0800 (Singapore Standard Time) 
⠹ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPool AWS::Cognito::UserPool Mon Dec 07 2020 14:43:50 GMT+0800 (Singapore Standard Time) 
⠋ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    UserPool AWS::Cognito::UserPool Mon Dec 07 2020 14:43:53 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UserPool AWS::Cognito::UserPool Mon Dec 07 2020 14:43:52 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠏ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    UserPoolClient    AWS::Cognito::UserPoolClient Mon Dec 07 2020 14:43:58 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UserPoolClient    AWS::Cognito::UserPoolClient Mon Dec 07 2020 14:43:58 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_COMPLETE    UserPoolClientWeb AWS::Cognito::UserPoolClient Mon Dec 07 2020 14:43:58 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UserPoolClientWeb AWS::Cognito::UserPoolClient Mon Dec 07 2020 14:43:58 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UserPoolClient    AWS::Cognito::UserPoolClient Mon Dec 07 2020 14:43:56 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UserPoolClientWeb AWS::Cognito::UserPoolClient Mon Dec 07 2020 14:43:56 GMT+0800 (Singapore Standard Time)                            
⠙ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPoolClientRole AWS::IAM::Role Mon Dec 07 2020 14:44:02 GMT+0800 (Singapore Standard Time) 
⠸ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPoolClientRole AWS::IAM::Role Mon Dec 07 2020 14:44:03 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠸ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE UserPoolClientRole AWS::IAM::Role Mon Dec 07 2020 14:44:22 GMT+0800 (Singapore Standard Time) 
⠴ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    UserPoolClientLambda AWS::Lambda::Function Mon Dec 07 2020 14:44:28 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UserPoolClientLambda AWS::Lambda::Function Mon Dec 07 2020 14:44:27 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UserPoolClientLambda AWS::Lambda::Function Mon Dec 07 2020 14:44:27 GMT+0800 (Singapore Standard Time)                            
⠴ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPoolClientLambdaPolicy AWS::IAM::Policy Mon Dec 07 2020 14:44:33 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UserPoolClientLambdaPolicy AWS::IAM::Policy Mon Dec 07 2020 14:44:31 GMT+0800 (Singapore Standard Time)                            
⠦ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPoolClientLogPolicy    AWS::IAM::Policy Mon Dec 07 2020 14:44:54 GMT+0800 (Singapore Standard Time) 
CREATE_COMPLETE    UserPoolClientLambdaPolicy AWS::IAM::Policy Mon Dec 07 2020 14:44:51 GMT+0800 (Singapore Standard Time) 
⠧ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPoolClientLogPolicy AWS::IAM::Policy Mon Dec 07 2020 14:44:57 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠇ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE UserPoolClientLogPolicy AWS::IAM::Policy Mon Dec 07 2020 14:45:15 GMT+0800 (Singapore Standard Time) 
⠏ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UserPoolClientInputs Custom::LambdaCallout Mon Dec 07 2020 14:45:18 GMT+0800 (Singapore Standard Time) 
⠋ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    UserPoolClientInputs Custom::LambdaCallout Mon Dec 07 2020 14:45:22 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UserPoolClientInputs Custom::LambdaCallout Mon Dec 07 2020 14:45:22 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠙ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    IdentityPool AWS::Cognito::IdentityPool Mon Dec 07 2020 14:45:29 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS IdentityPool AWS::Cognito::IdentityPool Mon Dec 07 2020 14:45:28 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS IdentityPool AWS::Cognito::IdentityPool Mon Dec 07 2020 14:45:26 GMT+0800 (Singapore Standard Time)                            
⠙ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    IdentityPoolRoleMap AWS::Cognito::IdentityPoolRoleAttachment Mon Dec 07 2020 14:45:34 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS IdentityPoolRoleMap AWS::Cognito::IdentityPoolRoleAttachment Mon Dec 07 2020 14:45:34 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS IdentityPoolRoleMap AWS::Cognito::IdentityPoolRoleAttachment Mon Dec 07 2020 14:45:32 GMT+0800 (Singapore Standard Time)                            
⠙ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE amplify-myprojectamplifydemo-dev-172354-authmyprojectamplifydemo5a4834e7-Y8FLQDMPUIO8 AWS::CloudFormation::Stack Mon Dec 07 2020 14:45:37 GMT+0800 (Singapore Standard Time) 
⠹ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    UpdateRolesWithIDPFunction       AWS::Lambda::Function      Mon Dec 07 2020 14:46:00 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UpdateRolesWithIDPFunction       AWS::Lambda::Function      Mon Dec 07 2020 14:45:59 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS UpdateRolesWithIDPFunction       AWS::Lambda::Function      Mon Dec 07 2020 14:45:59 GMT+0800 (Singapore Standard Time)                            
CREATE_COMPLETE    authmyprojectamplifydemo5a4834e7 AWS::CloudFormation::Stack Mon Dec 07 2020 14:45:56 GMT+0800 (Singapore Standard Time)                            
⠸ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS UpdateRolesWithIDPFunctionOutputs Custom::LambdaCallout Mon Dec 07 2020 14:46:02 GMT+0800 (Singapore Standard Time) 
⠸ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    UpdateRolesWithIDPFunctionOutputs Custom::LambdaCallout Mon Dec 07 2020 14:46:07 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS UpdateRolesWithIDPFunctionOutputs Custom::LambdaCallout Mon Dec 07 2020 14:46:07 GMT+0800 (Singapore Standard Time) Resource creation Initiated
⠼ Updating resources in the cloud. This may take a few minutes...

UPDATE_COMPLETE                     amplify-myprojectamplifydemo-dev-172354 AWS::CloudFormation::Stack Mon Dec 07 2020 14:46:11 GMT+0800 (Singapore Standard Time) 
UPDATE_COMPLETE_CLEANUP_IN_PROGRESS amplify-myprojectamplifydemo-dev-172354 AWS::CloudFormation::Stack Mon Dec 07 2020 14:46:10 GMT+0800 (Singapore Standard Time) 
✔ All resources are updated in the cloud
```

### Step 5: Add Amplify and Amplify-React libraries to the ReactJS App
```
$ yarn add aws-amplify aws-amplify-react
```

### Step 6: Edit ./src/App.js
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

### Step 7: Test
```
$ yarn start
```

### Step 8: Add Hosting
```
$ amplify add hosting
? Select the plugin module to execute Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)
? Choose a type Manual deployment

You can now publish your app using the following command:

Command: amplify publish
```

### Step 9: Run Amplify Status
```
$ amplify status

Current Environment: dev

| Category | Resource name  | Operation | Provider plugin   |
| -------- | -------------- | --------- | ----------------- |
| Hosting  | amplifyhosting | Create    | awscloudformation |
| Auth     | myapp9099242c  | No Change | awscloudformation |


No amplify console domain detected
```

### Step 10: Run Amplify Publish
```
$ amplify publish
✔ Successfully pulled backend environment dev from the cloud.

Current Environment: dev

| Category | Resource name  | Operation | Provider plugin   |
| -------- | -------------- | --------- | ----------------- |
| Hosting  | amplifyhosting | Create    | awscloudformation |
| Auth     | myapp9099242c  | No Change | awscloudformation |
? Are you sure you want to continue? Yes
⠋ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS hostingamplifyhosting    AWS::CloudFormation::Stack Fri Jun 19 2020 14:35:49 GMT+0800 (Singapore Standard Time)               
UPDATE_IN_PROGRESS amplify-myapp-dev-133155 AWS::CloudFormation::Stack Fri Jun 19 2020 14:35:44 GMT+0800 (Singapore Standard Time) User Initiated
⠏ Updating resources in the cloud. This may take a few minutes...

UPDATE_COMPLETE    authmyapp9099242c     AWS::CloudFormation::Stack Fri Jun 19 2020 14:35:52 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS hostingamplifyhosting AWS::CloudFormation::Stack Fri Jun 19 2020 14:35:51 GMT+0800 (Singapore Standard Time) Resource creation Initiated
UPDATE_IN_PROGRESS authmyapp9099242c     AWS::CloudFormation::Stack Fri Jun 19 2020 14:35:50 GMT+0800 (Singapore Standard Time)                            
⠙ Updating resources in the cloud. This may take a few minutes...

CREATE_IN_PROGRESS amplify-myapp-dev-133155-hostingamplifyhosting-1CWT5XVBR1OJ2 AWS::CloudFormation::Stack Fri Jun 19 2020 14:35:51 GMT+0800 (Singapore Standard Time) User Initiated
⠹ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE    AmplifyBranch AWS::Amplify::Branch Fri Jun 19 2020 14:35:59 GMT+0800 (Singapore Standard Time)                            
CREATE_IN_PROGRESS AmplifyBranch AWS::Amplify::Branch Fri Jun 19 2020 14:35:58 GMT+0800 (Singapore Standard Time) Resource creation Initiated
CREATE_IN_PROGRESS AmplifyBranch AWS::Amplify::Branch Fri Jun 19 2020 14:35:56 GMT+0800 (Singapore Standard Time)                            
⠧ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE amplify-myapp-dev-133155-hostingamplifyhosting-1CWT5XVBR1OJ2 AWS::CloudFormation::Stack Fri Jun 19 2020 14:36:00 GMT+0800 (Singapore Standard Time) 
⠸ Updating resources in the cloud. This may take a few minutes...

CREATE_COMPLETE hostingamplifyhosting AWS::CloudFormation::Stack Fri Jun 19 2020 14:36:02 GMT+0800 (Singapore Standard Time) 
⠋ Updating resources in the cloud. This may take a few minutes...

UPDATE_COMPLETE                     amplify-myapp-dev-133155 AWS::CloudFormation::Stack Fri Jun 19 2020 14:36:08 GMT+0800 (Singapore Standard Time) 
UPDATE_COMPLETE                     authmyapp9099242c        AWS::CloudFormation::Stack Fri Jun 19 2020 14:36:07 GMT+0800 (Singapore Standard Time) 
UPDATE_COMPLETE_CLEANUP_IN_PROGRESS amplify-myapp-dev-133155 AWS::CloudFormation::Stack Fri Jun 19 2020 14:36:06 GMT+0800 (Singapore Standard Time) 
✔ All resources are updated in the cloud


Publish started for amplifyhosting
yarn run v1.22.4
$ react-scripts build
Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

  134.06 KB  build/static/js/2.8c1f6e73.chunk.js
  3.63 KB    build/static/css/2.44a8782a.chunk.css
  849 B      build/static/js/main.e2d61853.chunk.js
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

✨  Done in 54.51s.
✔ Zipping artifacts completed.
✔ Deployment complete!
https://dev.d2ceyb8rq1u3g.amplifyapp.com
```

### (Optional) Cleanup
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
