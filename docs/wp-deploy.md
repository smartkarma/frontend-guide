# Wordpress deploy

## Nimbus

Is serving testing environments:

```
- staging
- build
```

!> Deploy first on `staging/build` to test any core changes or upgrades of wordpress

## Stratus

Used for production.

## Updating Wordpress

When using submodules. Sometimes it will have uncommited `wordpress`, to solve this issue run: `git submodule update`.
If this command fails, make sure that `wordpress` repo has all tags with: `git fetch --tags`.
