# Deploying
Guide how to publish/deploy our native app to [iTunes Connect](https://itunesconnect.apple.com).

Currently does not include guide how to submit app to iTunes Store.

---

# Deploying with Fastlane
> This manual assumes that you already gone through first time installation on [sk-native-app repo](https://github.com/smartkarma/sk-native-app#install-fastlane-and-dependencies)

?> Make sure you finished all feature branches and your master&develop is up to date.

1. Create new **release** with GitFlow
2. Increase app version in those files:
  - `package.json`
  - `ios/SKNativeApp/Info.plist` - version is in this key `<CFBundleShortVersionString>`
  - do the same for `SKNativeTests` folder as well.
3. run `yarn fastlane:beta` -- continue after fastlane is finished
4. commit all changed files with this message: `Release vX.X.X`
5. Finish **release** with GitFlow

!> Please always write notes about changes you are publishing/deploying

## Write changelog & Github release
1. Go to iTunes Connect and click on your build, write description
2. Go to Github repo, click on releases and choose your version tag and create new release.

---

# Manual deploying
!> This should be done only in case when you are not able to deploy with Fastlane

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
