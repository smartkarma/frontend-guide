# Updating Wordpress and 3rd party

## Theme Updating

> Guide for bought themes from themeforest

1.  Download latest version (also check changelog)
2.  Unpack .zip with theme
3.  Delete current theme files and add new one
4.  Check for plugins folder

* in case plugins folder exist, unpack all plugins and move them to `/assets/plugins`

!> Currently child theme is used so after updating we need to merge overridden files

Go to `salient-child` folder and check all files, whenever there is file which also exist in `salient` it will get overridden. So after each update we need to make sure that file has the new changes from parent and also persist our custom changes made.

> TIP: to make things easier, make a diff of parent vs. child file before updating to understand changes which were made.

## Wordpress updating

?> Make sure you are in `sk-wordpress` folder

1.  `cd wordpress`
2.  `git fetch`, `git fetch --tags`
3.  Find latest version of wordpress on wordpress.org
4.  `git checkout X.X.X` - X.X.X is the version you want to upgrade to
5.  Commit changes on `sk-wordpress` git
6.  Proceed with testing&deploy
7.  Once deployed go to Wordpress Site Admin and `Upgrade All Sites`
