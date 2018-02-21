## First time setup

### Prerequisites
* [Git](https://git-scm.com/)
* [Node.js](https://nodejs.org/)
* [Yarn^1.0](https://yarnpkg.com/)
* XCode - install through App Store

### 1. install npm packages
in `root` folder, run:
```bash
yarn
```

### 2. install cocoapods
go to `ios` folder and run:
```bash
sudo gem install cocoapods
pod install
```


After successful installation of all packages, open XCode and choose this build Scheme `SKNativeAppStaging`
![](https://cl.ly/0b1B3w3a3n2h/Screen%20Shot%202017-10-12%20at%205.35.03%20PM.png)


!> After installing all dependencies, copy the `.env.example` file to `.env.staging`. Otherwise all network request will fail.

## Run development server

```bash
yarn start
```

?> Most of the time, packager from `yarn start` will fail, so `yarn serve` is always needed

```bash
yarn serve
```

## Debugging

#### Useful shortcuts
* Open debug on simulator by `CMD + D`
* Toggle slow animation with `CMD + T`

#### React Native Debugger
Essential tool, to debug: **Redux, React code, JS/Network debugging**
* Install [react-native-debugger](https://github.com/jhen0409/react-native-debugger) with command
`brew update && brew cask install react-native-debugger`
* Enable Remote Debugging (this will automatically open react-native-debugger)

