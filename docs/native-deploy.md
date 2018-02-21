# Deploying
Guide how to publish/deploy our native app to [iTunes Connect](https://itunesconnect.apple.com).

Currently does not include guide how to submit app to iTunes Store.

---

# Bitrise.io
> CI tool that takes care of building and distributing app to TestFlight.

App is build from `develop` branch every day at **8pm**.
Link to install latest app version, can be found in Slack `nativeapp` channel.

---

# Manual deploying
!> This should be done used only as Emergency situation.

1. **Make sure** you opened **SKNativeApp.xcworkspace**
2. Remove `localhost` from `<key>NSExceptionDomains</key>` in `ios/SKNativeApp/Info.plist`
3. Choose Scheme `SKNativeAppStaging`.
4. Choose Device `Generic iOS Device`.
5. Increase build number choose `SKNativeApp` and in tab `General` increase `Build` number below `Version`.

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
