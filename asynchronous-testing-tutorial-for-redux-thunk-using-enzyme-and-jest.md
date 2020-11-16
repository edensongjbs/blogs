# Async Testing for Redux-Thunk (with Jest and Chuck Norris)

## Talk about importance of TDD

When I'm working on a personal React project, I'm always tempted to cut to the chase and get right to coding the fun stuff: seeing my app concept come to life.  I'll try and get a quick UI up and running, verify that it's behaving as expected in the browser and call it a day.  Often times (especially with a simple project), this is fine.  There are those other times when things break unexpectedly and I'll be stuck digging back through my code in paintstaking detail trying to remind myself how a particular piece of state is being updated or how a particular component is being used, all the while cursing myself for not starting out the project with a more rigorous test-driven approach.

Test driven development (TDD) always feels like a lift in the beginning stages of a project, but can end up saving so much time down the road.  It forces us to do the mental work up front, more rigorously planning the different components and their responsibilities, how these components will use state and how that state will be updated.  It lets us determine what is essential to the structure and function of our app, while abstracting away the implementation details that we can refactor as we go.  It provides us a failsafe, letting us know immediately if we modifeid something that's going to break the app.   Beyond this, it makes collaboration and communication easier in the longrun.  Being able to successfully test an app requires that we're able to clearly understand, codify, and communicate how the app should be working.  

## Challenges of Asynchronous Testing

For testing in React, I've primarily been using the Jest testing framework (which comes pre-installed in any new project created with `npx create-react-app`).  The [API Docs]() are well-written and the syntax (describe, test, expect) felt quite familiar to me coming from Rspec in Ruby.  Nevertheless, testing JavaScript poses some interesting challenges, especially when it comes to handling asynchronous functions.  While there are endless examples of those in any given JS/React project, I'm going to focus this article on how to do asynchronous testing with Redux-Thunk action creators, something I've found particularly challenging to wrap my head around.

If you're unfamiliar with Redux-Thunk, I'd recommend checking out [this post](https://www.digitalocean.com/community/tutorials/redux-redux-thunk#:~:text=Redux%20Thunk%20is%20a%20middleware,asynchronous%20operations%20have%20been%20completed.).  In short, Redux-Thunk allows for dispatching an asynchronous action, by letting you call an action creator that returns a function (instead of an action object), into which the store's dispatch function is passed.  The passed dispatch function is then used to dispatch standard synchronous action objects from within the function (either synchronously or asynchronously).

To help me demonstrate some Redux-Thunk testing techniques in Jest, I'll call upon everyone's favorite hyperbolic tough guy, Chuck Norris, to lend a hand...

## The App

I've build an exceedingly simple React/Redux app to demo our tests (you can find the GitHub repo [here]()).  In short, the app is a front-end for the [ChuckNorris.io API](https://api.chucknorris.io/), where the user will click a button and a random Chuck Norris 
"fact" will be displayed on the screen.  Important to our implementation is the detail that the user can only fetch up to 5 Chuck Norris "facts" before being cut off and being forced to refresh the page.  Though it's overkill in the extreme to be using Redux for such a simple app, it seems appropriately in the spirit of Chuck Norris and certainly a good opportunity to demo testing techniques without too many complicating factors. 

**Show the App GIF**

Here's a step by step for following along at home:

## Installing Dependencies

After creating a new react app (via `npx create-react-app [app-name]`), you'll need to install the following dependencies to get things set up:

`npm install --save-dev fetch-mock` ( to mock the API fetch request so that we can test our app in isolation )
`npm intall --save-dev node-fetch` ( since the tests will be using the fetch API without the browser )
`npm install redux react-redux redux-thunk` ( since the app uses redux and redux-thunk)

## Setting Up the App

## The Components

I've set up the App to render two components: a FetchButton component, that the user will click in order to fetch the new Chuck Norris "fact" and the Joke component, which will display the fact if it is successfully fetched.  The Joke button is purely presentational and receives the joke passed down in props from our App component.  However, the FetchButton component has access to our Redux store and will invoke our Redux-Thunk action creator fetchJoke, when the button is clicked.  

`paste in the various components`

## The Reducers

I set up our root Reducer to manage 3 distinct pieces of state: joke (the joke fetched from the API), jokeCount (the number of jokes that have fetched from the API since the program launched, which cannot exceed 5), tooMany (initially set to false, but set to true once the user attempts to fetch more jokes than allowed).

`paste in various reducers`

## Configuring and Connecting the Store to our App

You can refer to the [Redux-Thunk API docs]() for additional details on configuring the redux thunk middleware, but make sure to export your configured store so that it can be accessed for both testing and development/production purposes.  This is how I approached my storeFactory.

from ./src/configureStore.js
`import { createStore, applyMiddleware } from 'redux'
import ReduxThunk from 'redux-thunk'
import rootReducer from './reducers'

const storeFactory = (initialState) => {
    const middleware = [ReduxThunk]
    const createStoreWithMiddleware = applyMiddleware(...middleware)(createStore)
    return createStoreWithMiddleware(rootReducer, initialState)
}

export default storeFactory`

You'll need to pass your store to your App component and also import the storeFactory function into your test file, where you will use it to create a mock store for your tests.

in ./src/index.js (creating a store for the app)
`import store from './configureStore'

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store()}><App /></Provider>
  </React.StrictMode>,
  document.getElementById('root')
)`


## Setting Up The Action Creator and Tests

At the heart of the App's functionality, is a single aynchronous action creator called fetchJoke, which returns a function into which the store's dispatch function is passed.  This function will be responsible for dispatching other actions to our reducer.  It's very important for us to think through the logic of how these actions will be dispatched, as certain actions may be synchronous and others asynchronous, which will affect how we must structure our tests.

Let's jump now to setting up those tests.  For the purpose of this article, we're mostly concerned with setting up tests for our fetchJoke action creator.  This is technically an integration test, since it will be utilizing our reducers as well, but I decided to place it in our actions folder and name it accordingly since it's primary purpose is to test the action creator, the main logical component of our app.

Here are our test descriptions:

`paste in describe, and test without coding out the tests`

Before we can code out the test blocks, we need to do some preliminary setup in our `./src/actions/index.test.js` file:

## Step 1 - Create a Test Store

Since we have already created a storeFactory function, we can just import that and use it to create a mock store for our tests.

in .src/actions/index.test.js (creating a mock store for our tests)

`import createTestStore from '../configureStore'`


## Step 2 - Mocking the API Call

While our actual app relies upon fetching values from the ChuckNorris.io API, we want to test our app in isolation.  So, we'll need to sub in a mock fetch in place of the real fetch in the action creator.  We can do this purely in the test file without making any changes to our actual action creator code (ie) the app never needs to know that it's not getting a real API response).  We can do this with a useful tool call fetch-mock (that we've already installed as a dependency).  You can configure it like this:

`paste in the beforeEach and afterEach`

## Step 3 - Writing out the Test Blocks





## Return a Promise in the test 

Know when to return a promise and when not to.  Certain tests (and certain cases in action creator) require Async and some do not.  Explain why.

* Also must make sure to return the promise from action creator!!!

* Talk about how some tests must be set up asynchronously and some synch and why tests will fail unexpectedly if this is not done.  Requires implementation planning.

## Coding our Action Creator to Pass the tests