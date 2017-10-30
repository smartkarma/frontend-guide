# Publish Ember App
!> **don't forget `sk-common` to be on `master`** + pull develop&master branches.


### UPDATE SK-COMMON:
If needed, (everything done in feature branch)
  - change `sk-common` version number in `package.json`
  - run `yarn`, to change the `.lock` file.
  - commit message: `use sk-common vX.X.X`


### FINISH FEATURE BRANCH
> This step might not be needed, if you already finished your feature branch

  1. finish feature branch [this will merge branch to develop]


### CREATE NEW RELEASE
  use: `skrelease` script in git folder you want to make a release. [DOWNLOAD SCRIPT](https://gist.github.com/luisliuchao/07e2f32f7fffd1b11a03d25ea9df8031)

  ————— OR —————————————————————

  1. start release on develop branch
  2. change version number in `package.json`
  3. commit changes. Commit message: `Release vX.X.X`
  4. finish release

### DEPLOY
1. checkout to master [only when manualy released]
2. run: `ember deploy production --activate`
