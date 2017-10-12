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

## Publish

**Currently we publish to Apple TestFlight.**

1. Remove `localhost` from `<key>NSExceptionDomains</key>` in `ios/SKNativeApp/Info.plist`
2. Choose Scheme `SKNativeAppStaging`.
3. Choose Device `Generic iOS Device`.
4. Increase build number choose `SKNativeApp` and in tab `General` increase `Build` number below `Version`.

```bash
# Generate main.jsbundle inside 'ios/SKNativeApp'
yarn bundle
```

After that, go to XCode and add `main.jsbundle` to `SKNativeApp` folder.

![](https://cl.ly/120g0V3V1E0b/[16f594fbdd79f450616dc4e595fbfb50]_Image%202017-10-12%20at%205.51.36%20PM.png)

Finally build whole app within XCode by going to `Product > Archive`

Build will be uploaded to [iTunes Connect > TestFlight](https://itunesconnect.apple.com).
It will take few minutes to process build. After that it's needed to accept legal terms for each new build.

?> For those archiving for the first time. Ask someone from tech-team for certificates, which are required.

!> Don't forget to add back `localhost` to `<key>NSExceptionDomains</key>` in `ios/SKNativeApp/Info.plist`
