# Publish Ember App

## Preparation

* public key setup by your teammate in server
* `.env.deploy.build` settings ready from your teammate

## Deploy

!> Make sure `sk-common` is at the master branch with the same version number in `package.json`

1. checkout to master [only when manualy released]
2. run: `ember deploy build --activate` [environment could be `staging` or `production`]
3. update the **frontend update** in the foundry if necessary
