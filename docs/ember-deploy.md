# Publish Ember App

## Requirements

* Have your public key (mostly `id_rsa.pub`) at:
  * `nimbus.smartkarma.com`
  * `stratus.smartkarma.com`
* Properly fill `.env` files:
  * `.env.deploy.production`
  * `.env.deploy.staging`
  * `.env.deploy.build`

## Deploy

### Staging or Build

Just run `ember deploy build|staging --activate`

### Production

!> Only run from `master` branch, after finished GIT Flow Release

1. Check if web is working properly on your localhost
2. Run: `ember deploy production --activate`
3. If u introducing new changes, please fill the [frontend updates](https://foundry.smartkarma.com/frontend-updates)

## Past revisions

To deploy past revision do the following:

1. List past revisions using `ember deploy:list build|staging|production`
2. Activate a revision by running `ember deploy:activate build|staging|production --revision=<REVISION>`
