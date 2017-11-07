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

