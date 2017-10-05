# Deploying
Here you find instructions how to deploy all our frontend projects. Yes, even including React Native,
which is kinda considered as a frontend! 👍

# Publish Native App to EXPO

To publish your [DEV] or feature-branch to EXPO use this command:
```bash
yarn publish:expo
```

?> For more information please read `package.json` and following folder `build/`

---

# Publish Ember App
### DEPLOY PRODUCTION
!> **dont forget sk-common to be on master** + pull develop&master branches.


### UPDATE SK-COMMON:
If needed, (everything done in feature branch)
  - change sk-common version number in `package.json`
  -  run `yarn`, to change the `.lock` file.
  - commit message: `use sk-common vX.X.X`


### FINISH FEATURE BRANCH
  1. finish feature branch [this will merge branch to develop]


### CREATE NEW RELEASE
  use: `skrelease` script in git folder you want to make a release

  ————— OR —————————————————————

  1. start release on develop branch
  2. change version number in `package.json`
  3. commit changes. Commit message: `Release vX.X.X`
  4. finish release

### DEPLOY
1. checkout to master [only when manualy released]
2. run: `ember deploy production —activate`
