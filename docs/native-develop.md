# Install dependencies 

```
yarn install
cd ios
pod install
```

# Develop

You need to make sure `Exception Domains` in `ios/SKNativeApp/Info.plist` value is `localhost`.

Chose Scheme to build `SKNativeAppStaging`.

```
yarn start
```

If you have error when run this you can try to close the server window. And run this command.

```
yarn serve --reset-cache
```

## Note

If you want to install some native package and it require link you should do `react-native link ${package-name}` do not use `react-native link`.

# Release

You need to make sure `Exception Domains` in `ios/SKNativeApp/Info.plist` value is empty ``.

Choose Scheme to build `SKNativeAppStaging`.

Choose Device `Generic iOS Device`.

Increase build number (If you forget this you need to do Archive again) choose `SKNativeApp` and in tab `General` increase `Build` number below `Version`.

Generate `main.jsbundle` this file will contain all of js code and put inside `ios/SKNativeApp/` by this command.

```
yarn bundle
```

After generate `main.jsbundle` add that file to `SKNativeApp` use XCode to Archive an `ipa` file and upload to testflight.

```
Product -> Archive
```

Wait till it done and upload to Testflight.


