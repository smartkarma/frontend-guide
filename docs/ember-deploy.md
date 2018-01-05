# Publish Ember App

## Requirements

* have your public key (mostly `id_rsa.pub`) at:
  * nimbus.smartkarma.com
  * stratus.smartkarma.com
* properly filled `.env` files:
  * `.env.deploy.production`
  * `.env.deploy.staging`
  * `.env.deploy.build`

## Deploy

### Staging or Build

Just run `ember deploy build|staging --activate`

### List past revisions
`ember deploy:list build|staging`

### Activate past revisions
`ember deploy:activate build|staging --revision=<REVISION>`

### Production

!> Only run from `master` branch, after finished GIT Flow Release

1. Check if web is working properly on your localhost
2. Run: `ember deploy production --activate`
3. If u introducing new changes, please fill the [frontend updates](https://foundry.smartkarma.com/frontend-updates)
