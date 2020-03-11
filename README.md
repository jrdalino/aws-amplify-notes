# aws-amplify-notes
- https://aws.amazon.com/amplify/console/getting-started/?nc=sn&loc=3
- https://github.com/aws-samples/create-react-app-auth-amplify
- https://dev.to/dabit3/the-complete-guide-to-user-authentication-with-the-amplify-framework-2inh
- https://www.amplifyauth.dev/
- https://github.com/dabit3/amplify-auth-demo
- https://github.com/dabit3/aws-amplify-workshop-react
- https://github.com/dabit3/awesome-aws-amplify

## Getting Started (React)
### Step 1: Install Amplify CLI
```
$ npm install -g @aws-amplify/cli
$ amplify configure
```

### Step 2: Create a new app and install Amplify
```
$ npx create-react-app myapp
$ cd myapp
$ npm install @aws-amplify
$ npm start
$ npm install aws-amplify-react
```

### Step 3: Set up your backend and verify
```
$ amplify init
$ amplify status
```

### Step 4: Add API and Database
```
$ amplify add api
$ amplify push
```

### Step 5: Integrate into your app. Update src/App.js
- configure library with Amplify.configure
- add data to your database with a mutation by using API.graphql():
- list all the items in the database by importing listTodos and then using Hooks to update the page when a query runs on app start by adding initial state and a reducer function as well as modifying your App function:
- import the onCreateTodo subscription and create a new subscription by adding subscription with API.graphql()
```
import React, { useEffect, useReducer } from 'react';

import API, { graphqlOperation } from '@aws-amplify/api';
import PubSub from '@aws-amplify/pubsub';

import { createTodo } from './graphql/mutations';
import { listTodos } from './graphql/queries';
import { onCreateTodo } from './graphql/subscriptions';

import awsconfig from './aws-exports';
import './App.css';

API.configure(awsconfig);
PubSub.configure(awsconfig);

// Action Types
const QUERY = 'QUERY';
const SUBSCRIPTION = 'SUBSCRIPTION';

const initialState = {
  todos: [],
};

const reducer = (state, action) => {
  switch (action.type) {
    case QUERY:
      return {...state, todos: action.todos};
    case SUBSCRIPTION:
      return {...state, todos:[...state.todos, action.todo]}
    default:
      return state;
  }
};

async function createNewTodo() {
  const todo = { name: "Use AWS AppSync", description: "RealTime and Offline" };
  await API.graphql(graphqlOperation(createTodo, { input: todo }));
}

function App() {
  const [state, dispatch] = useReducer(reducer, initialState);

  useEffect(() => {
    async function getData() {
      const todoData = await API.graphql(graphqlOperation(listTodos));
      dispatch({ type: QUERY, todos: todoData.data.listTodos.items });
    }
    getData();

    const subscription = API.graphql(graphqlOperation(onCreateTodo)).subscribe({
      next: (eventData) => {
        const todo = eventData.value.data.onCreateTodo;
        dispatch({ type: SUBSCRIPTION, todo });
      }
    });

    return () => subscription.unsubscribe();
  }, []);

  return (
    <div className="App">
      <button onClick={createNewTodo}>Add Todo</button>
      <div>
        {state.todos.length > 0 ? 
          state.todos.map((todo) => <p key={todo.id}>{todo.name} : {todo.description}</p>) :
          <p>Add some todos!</p> 
        }
      </div>
    </div>
  );
}

export default App;
```

###
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

