# Testing

We use [Detox](https://github.com/wix/detox) for end to end testing with real devices.  We also use [Jest](https://github.com/facebook/jest) 
for writing unit tests for our reducers, components, utilities, etc.

## e2e testing (Detox) 

Let's follow part of the [Getting Started](https://github.com/wix/detox/blob/master/docs/Introduction.GettingStarted.md) docs from Detox:

### Setup

#### 1. Install the latest version of Homebrew

Homebrew is a package manager for macOS, we'll need it to install other command line tools.

> TIP: Verify it works by typing in terminal `brew -h` to output list of available commands

#### 2. Install Node.js

Node is the JavaScript runtime Detox will run on. **Install Node 7.6.0 or above for native async-await support**

 ```sh
 brew update && brew install node
 ```

> TIP: Verify it works by typing in terminal `node -v` to output current node version, should be higher than 7.6.0

#### 3. Install appleSimUtils

A collection of utils for Apple simulators, Detox uses it communicate with the simulator.

```sh
brew tap wix/brew
brew install --HEAD applesimutils
```

> TIP: Verify it works by typing in terminal `applesimutils` to output the tool help screen

#### 4. Install Detox command line tools (detox-cli)

This package makes it easier to operate Detox from the command line. `detox-cli` should be installed globally, enabling usage of the command line tools outside of your npm scripts.

  ```sh
  npm install -g detox-cli
  ```
> TIP: Verify it works by typing in terminal `detox -h` to output the list of available commands

### Build and run tests

Build:

```sh
yarn test:e2e:build
```

Run e2e test using:

```sh
yarn test:e2e
```

By default the app is removed, reinstalled and launched before each run. Starting fresh is critical in CI but in dev you might be able to save time between test runs and reuse the app that was previously installed in the simulator. To do so use the reuse flag and run your tests like this:

```sh
yarn test:e2e --reuse
```

### Write e2e tests

Here are all docs you need: [API Reference](https://github.com/wix/detox/blob/master/docs/README.md#api-reference). Example test:

```js
it('should log in correctly', async () => {
    await element(by.id('login-email')).typeText('someUsername');
    await element(by.id('login-password')).typeText('somePassword');
    await element(by.id('login-button')).tap();
    await expect(element(by.id('home-container'))).toExist();
});
```

If you want to access and `element(by.id('some-id'))`, you need to specify a `testID` to that element. Example:

```jsx
<View testID="home-container" />
```

Therefore, if you use any external library, it would be better we make sure they support `testID`.

## Unit testing (Jest)

Jest [docs](http://facebook.github.io/jest/docs/en/getting-started.html) have everything you need. 
Here we summarize the most useful features for us. 

To run all tests:

```sh
yarn test
```

You can also use `watch` or run only one test instead of several. Examples:

```sh
yarn test --watch
yarn test --watch myFile.test.js
yarn test --watch reducers/__tests__/toast.test.js
```

### Considerations

#### mockClear and mockReset

You do not need to recreate your mocks. Use [mockClear](http://facebook.github.io/jest/docs/en/mock-function-api.html#mockfnmockclear) 
or [mockReset](http://facebook.github.io/jest/docs/en/mock-function-api.html#mockfnmockreset) instead (usually in the `beforeEach` hook).

#### More specific expects

Imagine a case where we want to detect that a function has been called. We prefer more specific methods:

```js
expect(ourFunction).toBeCalled(); // This is true
expect(ourFunction).toHaveBeenCalledTimes(1); // This is also true but more specific
```

Check also for parameters if applies:

```js
expect(ourFunction).toBeCalledWith('banana');
```

### Testing functions

Pure functions are easy to test. We should aim to have functions that produce the same output for the same input without side effects. Example test:

```js
import marketCapText from '../market-cap';

test('marketCapText', () => {
  expect(marketCapText(null, null)).toEqual('All market caps');
  expect(marketCapText(0, null)).toEqual('All market caps');
  expect(marketCapText(null, 1)).toEqual('≤ 1 USDm');
  expect(marketCapText(1, 0)).toEqual('≥ 1 USDm');
  expect(marketCapText(1, 1)).toEqual('1 USDm');
  expect(marketCapText(1, 3)).toEqual('1 – 3 USDm');
});
```

### Testing reducers

Reducers are just pure functions, so testing them is as easy as:

```js
it('handles Toast/SHOW_TOAST', () => {
  const newState = toastReducer(undefined, { type: 'Toast/SHOW_TOAST', ...testToast });
  expect(newState).toEqual({ toasts: [testToast] });
});
```

### Testing components

Components without state are easy to test. We just need to test the render function and its output. We can use
[Snapshots](https://facebook.github.io/jest/docs/en/snapshot-testing.html) or a more manual method using 
[Enzyme](http://airbnb.io/enzyme/).

With Snapshots we can generate the full component tree:

```js
expect(renderer.create(baseComponent)).toMatchSnapshot();
```

We can use then [snapshot-diff](https://github.com/jest-community/snapshot-diff) to snap differences:

```js
expect(baseComponent).toMatchDiffSnapshot(
  <Timestamp format={'YYYY-MM'} value={'2017-10-26T17:31:06.862+08:00'} />,
  { contextLines: 0 }
);
```

With Snapshots you will generate `.snap` files which should be also committed and reviewed.

With Enzyme, it takes some more manual work:

```js
import { shallow } from 'enzyme';

const wrapper = shallow(baseComponent);
expect(
  wrapper
    .find(FontAwesome)
    // Quite nested
    .dive()
    .dive()
    .text()
).toEqual('');
expect(wrapper.contains('26 Oct 2017 11:31')).toBe(true);
```

However, Snapshots and Enzyme can be used together. Actually, we need Enzyme to interact with the component
(clicking a button, change state, change props...). Refer to [Enzyme api docs](http://airbnb.io/enzyme/docs/api/).