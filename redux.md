* yarn add `redux` for state management
* yarn add `redux-react` for React bindings
* yarn add `redux-actions` to create [FSA](https://github.com/acdlite/flux-standard-action) compliant actions
* yarn add `redux-devtools` for development tools support, or install the [Redux DevTools Extension](https://github.com/zalmoxisus/redux-devtools-extension) instead
* yarn add `redux-logger` for basic logging middleware
* yarn add `redux-thunk` to create basic asynchonous actions
* yarn add `redux-observable` or `redux-saga` for more advanced asynchronous scenarios
* yarn add `immutable` for easier development of reducers and performance benefits 
  * Follow [ImmutableJS best practices](http://redux.js.org/docs/recipes/UsingImmutableJS.html#immutable-js-best-practices)
* yarn add `redux-immutable` to use a `combineReducers` which supports an ImmutableJS object as the root state object
* yarn add `reselect` for creating selectors
* yarn add `normalizr` for normalizing your Redux state for easier management
* yarn add `react-router-redux` if you wish to sync react router with redux in order to time travel route changes 

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
