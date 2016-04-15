For huge Redux apps, you may want to split your reducers. This allows you to load them asynchonously
and separate your app into mini-redux apps for each route.

Why this vs. Relay? This method still supports server side rendering.

```javascript
// ./createReducer.js
import posts from './routes/PostList/reducer';
import { combineReducers } from 'redux';

// Only combine reducers needed for initial render, others will be
// added async
export default function createReducer(asyncReducers) {
  return combineReducers({
    posts,
    ...asyncReducers,
  });
}
```


```javascript
// ./configureStore.js
import { createStore, applyMiddleware, compose } from 'redux';
import thunk from 'redux-thunk';
import { callAPIMiddleware } from './middleware/callAPIMiddleware';
import createReducer from './createReducer';

export function configureStore(initialState = {}) {
  let store = createStore(createReducer(), initialState, compose(
    applyMiddleware(
      thunk,
      callAPIMiddleware
    ),

     (process.env.NODE_ENV === 'development') &&
      typeof window === 'object' &&
       typeof window.devToolsExtension !== 'undefined' ?
        window.devToolsExtension() : f => f
  ));

  store.asyncReducers = {};
  
  return store;
}

export function injectAsyncReducer(store, name, asyncReducer) {
  store.asyncReducers[name] = asyncReducer;
  store.replaceReducer(createReducer(store.asyncReducers));
}

```

```javascript
// Example lazy loaded route with async reducer
// ./routes/PostPage/index.js

if (typeof require.ensure !== 'function') require.ensure = (d, c) => c(require);
import { injectAsyncReducer } from '../../store';

export default function createRoutes(store) {
  return {
    path: 'post/:slug',
    getComponents(location, cb) {
      require.ensure([
          './containers/PostPage',
          './reducer',
        ], (require) => {
          let PostPage = require('./containers/PostPage').default;
          let postReducer = require('./reducer').default;
          injectAsyncReducer(store, 'currentPost', postReducer);
          cb(null, PostPage);
        });
    },
  };
}
```


