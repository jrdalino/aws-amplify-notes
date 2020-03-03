# aws-amplify-notes
- https://aws.amazon.com/amplify/console/getting-started/?nc=sn&loc=3
- https://github.com/aws-samples/create-react-app-auth-amplify
- https://dev.to/dabit3/the-complete-guide-to-user-authentication-with-the-amplify-framework-2inh
- https://www.amplifyauth.dev/
- https://github.com/dabit3/amplify-auth-demo

## Getting Started (React)
### Step 1: Intall Amplify CLI
```
$ npm install -g @aws-amplify/cli
$ amplify configure
```

### Step 1: Create a new app
```
$ npx create-react-app rn-amplify
$ cd rn-amplify
$ npm install @aws-amplify
$ npm start
$ npm install aws-amplify-react
```

### Step 2: Set up your backend
```
$ npm install aws-amplify-react
$ amplify status
```

### Step 3: Add API and Database
```
$ amplify add api
$ amplify push
```

### Step 4: Integrate into your app
```
$ amplify console api
```

### Step 5: Launch your app
```
$ amplify add hosting
$ amplify publish
```

## References
### AWS Amplify https://aws.amazon.com/amplify/
#### Features: https://aws.amazon.com/amplify/features/
#### Products
-	Framework > Overview: https://aws.amazon.com/amplify/framework/?nc=sn&loc=2&dn=1
- Framework > Style Guide: https://aws-amplify.github.io/media/ui_library
- Amplify Console > Overview: https://aws.amazon.com/amplify/console/?nc=sn&loc=2&dn=2
- Amplify Console > Pricing: https://aws.amazon.com/amplify/console/pricing/?nc=sn&loc=2
- Amplify Console > Getting Started: https://aws.amazon.com/amplify/console/getting-started/?nc=sn&loc=3
- Amplify Console > Documentation: https://docs.aws.amazon.com/amplify/latest/userguide/welcome.html
- Amplify Console > Forums: https://github.com/aws-amplify/amplify-console/issues
- AWS Device Farm: https://aws.amazon.com/device-farm/?nc=sn&loc=2&dn=3
#### FAQs: https://aws.amazon.com/amplify/console/faqs/?nc=sn&loc=5

### AWS Amplify Framework https://aws-amplify.github.io/
#### Get Started: https://aws-amplify.github.io/docs/
#### Style Guide: https://aws-amplify.github.io/media/ui_library
#### Docs (JavaScript): https://aws-amplify.github.io/docs/js/start?platform=purejs
#### API (JavaScript): https://aws-amplify.github.io/amplify-js/api/
#### Community: https://amplify.aws/community/

