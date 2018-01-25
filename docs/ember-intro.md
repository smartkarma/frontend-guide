# Introduction to our Ember platform

The whole Smartkarma Ember ecosystem consists of these projects:


### [smartkarma.com](https://www.smartkarma.com)

> Main project, called platform, web

* Repository: [smartkarma-web](https://github.com/smartkarma/smartkarma-web)
* Domains:
  * PRODUCTION
    * `www.smartkarma.com`
  * STAGING
    * `s.smartkarma.com`
    * `sk-web-staging.smartkarma.com`
  * BUILD
    * `b.smartkarma.com`
    * `sk-web-build.smartkarma.com`


### [foundry.smartkarma.com](https://foundry.smartkarma.com)

> Platform administration, statistics viewing, content management. **Only internal users have access**

* Repository: [sk-foundry](https://github.com/smartkarma/sk-foundry)
* Domains:
  * PRODUCTION
    * `foundry.smartkarma.com`
  * STAGING
    * `fs.smartkarma.com`
    * `sk-foundry-staging.smartkarma.com`
  * BUILD
    * `fb.smartkarma.com`
    * `sk-foundry-build.smartkarma.com`


### [smartkarma.com/home](https://www.smartkarma.com/home)

> Public/Landing page. For non-logged users, this is the web when they access `smartkarma.com`. For logged-in users, the same page is accessed under `smartkarma.com/home`.

?> This is running/using on Ember Fastboot

* Repository: [sk-public](https://github.com/smartkarma/sk-public)


## Shared internal libraries

### sk-common

> Includes common components, utilities, helpers, mixins used by: **sk-foundry** and **smartkarma-web**

* Repository: [sk-common](https://github.com/smartkarma/sk-common)
