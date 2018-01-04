# Development Process

## Dependencies

* git
* nvm
* yarn
* bower
* watchman
* ember-cli

## One time setup

1. Make sure u have all those repo cloned: `smartkarma-web, sk-foundry, sk-common, sk-public`.
2. `nvm use` (make sure u always use correct node version with `node -v`)
2. `yarn link` inside `sk-common` folder.
3. `yarn link sk-common` in `smartkarma-web, sk-foundry` folders.
4. `yarn && bower install` in all 4 repo mentioned above.


## Start local server

> Works for: smartkarma-web, sk-foundry

To run a local server for *smartkarm-web*, *sk-foundry* use following command:
```bash
yarn staging-proxy
```
?> U can also use: `build-proxy` to use BUILD API.

* **smartkarma-web** will be available at: [localhost:4200](http://localhost:4200)
* **sk-foundry** will be available at: [localhost:4200](http://localhost:4200)


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

## FAQ 😭
If something went wrong, please read those 🤗

### Yarn fails with sk-common

There are two most common issues:
1. Missing login for Github in terminal. Try `git fetch` inside terminal. If it works u can continue to 2nd.
  * after running command, GitHub will ask for username and password. Type your username, **but** for password, you need
  to use token (in case you use 2Factor Auth), which u can get [here](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
2. Not accepted Github RSA fingerprint to known-hosts, to get the dialog run this: `git ls-remote --tags --heads ssh://git@github.com/smartkarma/sk-common`
  * after that, just type `yes` to add fingerprint.

### How to get my SSH key

* Your key should be locate inside `cd ~/.ssh`, if that's not the case, please generate one for yourself with this command: `ssh-keygen -t rsa`.
* Quickly copy your public key: `cat ~/.ssh/id_rsa.pub | pbcopy`

### Deploy failed with auth error

In some cases, you might not have access to `sk-stratus` or `sk-nimbus` servers. Please verify u had a access by SSH those servers.
