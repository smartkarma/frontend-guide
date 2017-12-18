# Development Process

## Preparation

* git
* yarn
* bower
* nvm
* watchman

### Recommendation

* sourcetree / gitkraken
* iterm2
* oh-my-zsh

## Start the server

### sk-common

```bash
nvm use
yarn
bower install
yarn link
```

### smartkarma-web

```bash
nvm use
yarn
bower install
yarn link sk-common
npm run staging-proxy
```

open the browser tab and go to **localhost:4200**

### sk-foundry

```bash
nvm use
yarn
bower install
yarn link sk-common
npm run staging-proxy
```

open the browser tab and go to **localhost:4201**

## Feature development

### Start feature

1. start the feature branch with name followed the convention as `[pivot tracker ticker id]-[feature name separated with -]`
2. if there's any change in `sk-common`, create a new feature in `sk-common` with the same name

### Finish feature branch

!> Run `ember test` and make sure there is no test error before finishing any feature branch

!> Rebase to the latest `develop` branch before finishing the branch

!> Remember to check **browser compatibility** before finish branch related with UI

!> check whether the change in `sk-common` would affect other repo or not. If yes, update the other repo as well!

1. if there's any change in `sk-common`, [make a release](ember-develop?id=create-new-release) in `sk-common` first
2. change `sk-common` version number in `package.json`
3. run `yarn`, to change the `.lock` file.
4. commit message: `use sk-common vX.X.X`
5. finish feature branch [this will merge branch to develop]

## Hotfix

?> Releasing hotfix branch won't include the unreleased develop branch content

1. start a new hotfix branch with version number from `v1.0.0` to `v1.0.1` [increment the last digit]
2. commit the change
3. finish the hotfix and [deploy](ember-deploy?id=deploy)

## Release

!> **don't forget `sk-common` to be on `master`** + pull develop & master branches.

use: `skrelease` script in git folder you want to make a release. [DOWNLOAD SCRIPT](https://gist.github.com/luisliuchao/07e2f32f7fffd1b11a03d25ea9df8031)

————— OR —————————————————————

1. start release on develop branch
2. change version number in `package.json`
   * follow the [version semantic](https://semver.org/)
3. commit changes. Commit message: `Release vX.X.X`
4. finish release
