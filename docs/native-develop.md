## First time setup

```bash
yarn install
cd ios
pod install
```

?> Probably you don't have installed cococoa `pod`. To install run: `sudo gem install cocoapods`

After successful installation of all packages, open XCode and choose this build Scheme `SKNativeAppStaging`
![](https://cl.ly/0b1B3w3a3n2h/Screen%20Shot%202017-10-12%20at%205.35.03%20PM.png)

## Run development server

```bash
yarn start
```

If you are not able to run `yarn start`, please close the window and try this command:

```bash
yarn serve --reset-cache
```

!> Never run `react-native link` without specifying package name.

## Debugging

#### Useful shortcuts
* Open debug on simulator by `command + D`
* Toggle slow animation with `command + T`

For better debugging experience, we recommend to use React Native Debugger:
* Install [react-native-debugger](https://github.com/jhen0409/react-native-debugger) with command `brew update && brew cask install react-native-debugger`
* Enable Remote Debugging (this will automatically open react-native-debugger)

#### Debug network
All network request are logged to console, but for more refine control over network, please install **Reactotron**.
* Install [Reactotron](https://github.com/infinitered/reactotron)

Quick introduction to debugging of React Native apps:
* https://medium.com/reactnativeacademy/debugging-react-native-applications-6bff3f28c375
