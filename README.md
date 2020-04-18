# aws-amplify-notes

## Prerequsites: Install Amplify CLI
```
$ npm install -g @aws-amplify/cli
$ amplify configure
```

## Step 1: Create a new app, initialize and install Amplify
```
$ npx create-react-app myapp && cd myapp
$ amplify init
$ yarn start
```

## Step 2: Publish
```
$ amplify add hosting (DEV)
$ amplify status
$ amplify update hosting (PROD) 
```

## Step 3: Add Auth
```
$ amplify add auth
$ amplify push
$ yarn add aws-amplify aws-amplify-react
```
- ./src/App.js
```
import Amplify from 'aws-amplify';
import awsconfig from './aws-exports';
import { withAuthenticator } from 'aws-amplify-react'; // or 'aws-amplify-react-native';
import '@aws-amplify/ui/dist/style.css';

Amplify.configure(awsconfig);

...

export default withAuthenticator(App, true);
```

##  Step 4: Publish
```
$ amplify publish
```

## References
- React Getting Started: https://aws-amplify.github.io/docs/js/react
- Authentication Getting Started: https://docs.amplify.aws/lib/auth/getting-started?platform=js
- Authentication: https://aws-amplify.github.io/docs/js/authentication
