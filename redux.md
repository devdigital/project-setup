# Basics

* yarn add `redux` for state management
* yarn add `redux-react` for React bindings
* yarn add `redux-actions` to create [FSA](https://github.com/acdlite/flux-standard-action) compliant actions
* yarn add `redux-devtools` for development tools support, or install the [Redux DevTools Extension](https://github.com/zalmoxisus/redux-devtools-extension) instead
* yarn add `redux-logger` for basic logging middleware

# Async

* yarn add `redux-thunk` to create basic asynchonous actions
* yarn add `redux-pack` for cleaner promise based actions
* yarn add `redux-observable` 
* yarn add `redux-saga`

# Immutable

* yarn add `immutable` for easier development of reducers and performance benefits 
* yarn add `redux-immutable` to use a `combineReducers` which supports an ImmutableJS object as the root state object

Either:

1. Use `Record` which allows dot notation in presentational components
2. Use `fromJS()` on objects (`Map`) and collections (`List`), and use a higher order component to convert `toJS()` for your presentational components

The issue with `Record` is that nested `Record`s are difficult to deal with, so the HOC approach is preferred.

* Follow [ImmutableJS best practices](http://redux.js.org/docs/recipes/UsingImmutableJS.html#immutable-js-best-practices)

# Routing

* yarn add `react-router`
* yarn add `react-router-redux` if you wish to sync react router with redux in order to time travel route changes 

However, I prefer router 5:

* yarn add `router5`
* yarn add `react-router5`
* yarn add `redux-router5`

# Advanced

* yarn add `reselect` for creating selectors
* yarn add `normalizr` for normalizing your Redux state for easier management

# Store

Follow the [ducks](https://github.com/erikras/ducks-modular-redux) pattern for laying out your Redux components. See the [sample](https://github.com/erikras/react-redux-universal-hot-example/tree/master/src/redux):

* Create a `redux` folder within your root `src` folder. 
* In the root of the `redux` folder add a `create.js` file to create your Redux store:

```
import { createStore, applyMiddleware, compose } from 'redux';
import thunkMiddleware from 'redux-thunk';
import createLogger from 'redux-logger';
import reducer from '../reducers';

export default function configureStore(baseHistory, initialState) {
    const routingMiddleware = routerMiddleware(baseHistory);

    const store = createStore(
        reducer,
        initialState,
        compose(
            applyMiddleware(routingMiddleware, thunkMiddleware, createLogger()),
            window.devToolsExtension ? window.devToolsExtension() : f => f
        )
    );

    if (module.hot) {
        // Enable Webpack hot module replacement for reducers
        module.hot.accept('../reducers', () => {
            const nextRootReducer = require('../reducers').default;
            store.replaceReducer(nextRootReducer);
        });
    }

    return store;
}
```
