# Async Testing Techniques for Redux-Thunk (Jest/Enzyme)

## Talk about importance of TDD

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