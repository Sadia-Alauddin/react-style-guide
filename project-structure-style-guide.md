# ReactJS Guide
While writing react application keep these rules in mind.

React application can be quickly bootstrapped using [create-react-app](https://github.com/facebook/create-react-app)

## Coding

  - For typings use `flow` which is highly recommended by the reactjs community.
  - Use `eslint` as static code analyzer and for strict es6 and react rules use basic eslint and extend it with airbnb `eslint-config-airbnb`, it has extensive rules for both es6 and ReactJs.
  - All react component names should be `PascalCase`.
  - Api requests and other async requests in a react application sholud be made through actions using these middlwares or any other but these are the most used:
      - [redux-thunk](https://github.com/reduxjs/redux-thunk)
      - [redux-saga](https://github.com/redux-saga/redux-saga)
      - [redux-observable](https://github.com/redux-observable/redux-observable)
  - Import sequence in application should be in this order:
      - 3rd party libraries
      - Project dependencies
      - styles
  - For forms [Formik](https://github.com/jaredpalmer/formik) is the simple and best tool, it uses [Yup](https://github.com/jquense/yup) for validaiton.
  - For redux store logs [redux-logger](https://www.npmjs.com/package/redux-logger) is a good tool, it shows the state of redux store before and after any action is executed.
	
## Proptypes:

All the components should have proptypes. Proptypes should be defined in the component. If proptypes are shared between components and containers they can be moved to the proptypes direcotry. Avoid using proptypes.object and proptypes.any insted use proptype.shape and define proptypes.

## Containers:

Containers in a react application are also called smart components. All the business logic and data processing will be handled in the containers. Containers should know nothing about the rendering logic hence ideally they should'nt have a stylesheet file.

Redux connected containers can not have state of their own. A smart component can have only one state at a time either redux state or the components state.

## Components:

Componetns or Dumb components are those who know nothing about the business logic and only handle the viewing logic. Data and actions to a dumb component are passed from parents using attributes. All the styling of a component should be in a stylesheet file in the component folder. A component should be independent and must work if the required attributes are provided. Components can have their own sate if required. If a dumb component don't have state or any lifecycle methods it should be written as a pure funciton.

## Action Creators:

Actions creators in a react application should be pure functions. Their only task should be to return an action nothing else.
	
## Reducers:

Data in a react application can be processed either in the reducer or in a service file before setting it in the state.


## Directory structure
```bash
    ├── src
    │   ├── .eslintignore
    │   ├── .eslintrc.json
    │   ├── .gitignore
    │   ├── .sasslintrc
    │   ├── package.json
    │   ├── package-lock.json
    │   ├── README.md
    │   ├── app
    │   │   ├── actions
    │   │   │   ├── app.js
    │   │   │   └── user.js
    │   │   ├── components
    │   │   │   ├── App
    │   │   │   │   ├── index.js
    │   │   │   │   ├── index.scss
    │   │   │   │   └── app.test.js
    │   │   │   └── User
    │   │   │       ├── index.js
    │   │   │       ├── index.scss
    │   │   │       └── user.test.js
    │   │   ├── constants
    │   │   │   ├── user.js
    │   │   │   └── index.js
    │   │   ├── containers
    │   │   │   ├── AppContainer.js
    │   │   │   ├── appContainer.test.js
    │   │   │   ├── UserContainer.js
    │   │   │   └── userContainer.js
    │   │   ├── proptypes
    │   │   │   └── user.js
    │   │   ├── reducers
    │   │   │   ├── user.js
    │   │   │   └── index.js
    │   │   └── services
    │   ├── assets
    │   │   ├── fonts
    │   │   ├── images
    │   │   └── styles
    │   │       └── **/*.scss
    │   └── environment
    │       ├── index.js
    │       ├── prod.js
    │       ├── dev.js
    │       ├── staging.js
    │       └── qa.js
    └── ...
```

## Actions Structure:
```jsx
export const INCREMENT = 'INCREMENT';
export const DECREMENT = 'DECREMENT';

const increment = payload => ({
    type: INCREMENT,
    payload,
});

const decrement = payload => ({
    type: DECREMENT,
    payload,
});
```

## Reducer Structure:
```jsx
import { INCREMENT, DECREMENT } from actions;

const initialState = {
    counter: 0
}

export const count = (state = initialState, action) => {
    switch (action.type) {
    case INCREMENT:
        return {
            counter: initialState.counter += action.payload,
        };
    case DECREMENT:
        return {
            counter: initialState.counter -= action.payload,
        };
    default:
        return state;
    }
};
```


