# Async Testing Techniques for Redux-Thunk (Jest/Enzyme)

## Talk about importance of TDD

When I'm working on personal React projects, I'm always tempted to cut to the chase and get right to coding the fun stuff: seeing my app concept come to life.  I'll try and get a quick UI up and running, verify that it's behaving as expected in the browser and call it a day.  Often times (especially with a simple project), this is fine.  There are those other times when things break unexpectedly and I'll be stuck digging back through my code in paintstaking detail trying to remind myself how a particular piece of state is being updated or how a particular component is being used, all the while cursing myself for not starting out the projecrt with a more rigorous test-driven approach.

Test driven development (TDD) always feels like a lift in the beginning stages of a project, but can end up saving so much time down the road.  

## Challenges of Asynchronous Testing

## Installing Dependencies
- enzyme
- enzyme adapter
- fetch-mock (node-fetch required by fetch-mock)
- react-redux
- redux
- redux-thunk

## Setting Up the App

## Mocking the Store

    Issue # 1:
    Could not find "store" in the context of "Connect(App)". Either wrap the root component in a <Provider>, or pass a custom React context provider to <Provider> and the corresponding React context consumer to Connect(App) in connect options.


## Mocking the API Call

## Return a Promise in the test 

* Also must make sure to return the promise from action creator!!!

* Talk about how some tests must be set up asynchronously and some synch and why tests will fail unexpectedly if this is not done.  Requires implementation planning.