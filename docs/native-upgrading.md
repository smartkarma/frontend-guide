# Upgrading
Description how to upgrade our dependencies we use for native development.

# React native
`// FIXME`

# Flow
Flow should be upgrade after React Native (Flow version can be found in `package.json`)
1. Upgrade Flow with command: `yarn upgrade flow-bin@X.X.X`
2. Change version number in `.flowconfig`
3. Run `flow-upgrade`, which will try to fix all changes
4. Run `flow-typed install`, which will try to fetch newer version of flow-typed types

# Fastlane
1. `sudo gem install fastlane`
2. `bundle update fastlane`
