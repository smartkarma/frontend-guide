# Development Process 💯

## Dependencies

* git
* nvm
* yarn
* bower
* watchman
* ember-cli

## One time setup

1. Make sure you've the following repos cloned: `smartkarma-web`, `sk-foundry`, `sk-common`, `sk-public`
2. `nvm use` (make sure that you're using the correct node version with `node -v`)
2. `yarn link` inside `sk-common` folder
3. `yarn link sk-common` in `smartkarma-web` and `sk-foundry` folders
4. `yarn && bower install` in all 4 repos

## Start local server

> For `smartkarma-web` & `sk-foundry`

To run a local server for `smartkarma-web` or `sk-foundry` use following command:
```bash
yarn staging-proxy
```
?> You can also use: `yarn build-proxy` to connect to the `build` API

* `smartkarma-web` will be available at: [localhost:4200](http://localhost:4200)
* `sk-foundry` will be available at: [localhost:4200](http://localhost:4200)

## Feature development

### Start feature

1. Start a feature branch and name it using the following naming convention: `[pivotal tracker ticker id]-[feature name separated with -]`
  * Eg: `146673807-qva-analytics-report`
2. If there's any change in `sk-common`, create a new feature in `sk-common` with the same name

### Finish feature branch

!> Run `ember test` and make sure there's no test error before finishing the feature branch

!> Rebase to the latest `develop` branch before finishing the branch

!> Remember to check **browser compatibility** before finishing UI related branch

!> Check whether or not changes in `sk-common` affect other repos. If yes, update the other repo as well!

1. If there's any change in `sk-common`, [make a release](ember-develop?id=create-new-release) in `sk-common` first
2. Change `sk-common` version number in `package.json`
3. Run `yarn` to change the `.lock` file
4. Commit message: `use sk-common vX.X.X`
5. Finish the feature branch. This will **merge** the branch to `develop`

## Hotfix

?> Releasing a hotfix branch will not include unreleased `develop` branch content

1. Start a new hotfix branch with the incremented version number as the name
  * Eg: `v1.0.0` to `v1.0.1` [increment the last digit]
2. Commit the changes
3. Update `package.json` version number & commit with `Hotfix vX.X.X`
4. Finish the hotfix and [deploy](ember-deploy?id=deploy)

## Release

!> Don't forget `sk-common` to be on `master` & pull `develop` & `master` branches

You can make a release by either using a script or doing it manually

### Using a script

Use `skrelease` script in the folder you where want to make the release. Click [here](https://gist.github.com/luisliuchao/07e2f32f7fffd1b11a03d25ea9df8031) to download the script

### Manual release

1. Start a new release branch with the incremented version as the name using `vX.X.X` format
  * Eg. `v1.0.0` to `v1.0.1`
  * Follow the [version semantic](https://semver.org/)
2. Change the version number in `package.json`
3. Commit changes. Commit message: `Release vX.X.X`
4. Finish release and [deploy](ember-deploy?id=deploy)

## FAQ

If something went wrong, please read the following tips

### Yarn fails with sk-common

Two most common issues:
1. Missing login for Github in terminal. Try `git fetch` inside the terminal. If it works you can continue to 2<sup>nd</sup> step
  * After running the command, GitHub will ask for your username and password. Type your username, **but** for password, you need to use a token (in case you use 2Factor Auth), which you can get [here](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
2. Not accepted Github RSA fingerprint to known hosts, to get the dialog run this: `git ls-remote --tags --heads ssh://git@github.com/smartkarma/sk-common`
  * After that, just type `yes` to add the fingerprint

### How to get my SSH key

* Your key should be located inside `cd ~/.ssh`, if that's not the case, please generate one for yourself with this command: `ssh-keygen -t rsa`
* Copy your public key: `cat ~/.ssh/id_rsa.pub | pbcopy`

### Deploy failed with auth error

In some cases, you might not have access to `sk-stratus` or `sk-nimbus` servers. Please verify you have access by SSH those servers
