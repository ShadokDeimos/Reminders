
# REDUX

## ADD REDUX TO REACTJS PROJECT

npm install -s react-redux react-router-dom redux redux-actions redux-thunk connected-react-router react-router history

[Root]
|
|
_ _ [Redux]
		|
		rootReducer.js
		store.js
		|
		[ExmpReducer]

_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _

rootReducer.js

import { combineReducers } from 'redux'
import { connectRouter } from 'connected-react-router'
import adminReducer from './admin/reducers/index'

export default (history) => combineReducers({
    router: connectRouter(history),
    adminReducer,
})

__ __ __ __ __ __ __ __

store.js

import { createStore, applyMiddleware } from 'redux'
import { composeWithDevTools } from 'redux-devtools-extension'
import { routerMiddleware } from 'connected-react-router'
import thunk from 'redux-thunk'
import { createBrowserHistory } from 'history'
import rootReducer from './rootReducer'

export const history = createBrowserHistory()

const composeEnhancers = composeWithDevTools({
    // Specify name here, actionsBlacklist, actionsCreators and other options if needed
});

export default function configureStore(preloadedState) {
    const store = createStore(
        rootReducer(history),
        preloadedState,
        composeEnhancers(
            applyMiddleware(
                routerMiddleware(history),
                thunk
            )
        )
    )
    return store
}

__ __ __ __ __ __ __ __

index.js

import { Provider } from 'react-redux';
import { Route, Switch } from 'react-router';
import { ConnectedRouter } from 'connected-react-router';
import configureStore, { history } from './Redux/store';

const initialState = {};

const store = configureStore(initialState);

ReactDOM.render(
    <Provider store={store}>
        <ConnectedRouter history={history}>
            <Switch>
                <Route exact path="/" component={Login} />
                <Route path="/:login/dashboard" render={() => (<Main content={Dashboard} />)} />
            </Switch>
        </ConnectedRouter>
    </Provider>
    , document.getElementById('root')
);
