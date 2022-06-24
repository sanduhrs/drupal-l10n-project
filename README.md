# Drupal L10n Server - Development Setup

## Get the code

```
    git clone git@github.com:sanduhrs/drupal-l10n-project.git
    cd drupal-l10n-project
```

## Prerequisites

You need to have DDEV installed to follow the instructions.
https://ddev.com/get-started/

or a different working LAMP/LEMP-stack for Drupal.

## Run the server
```
    ddev start
```

Or just use your own development environment and strip the ddev prefixes from the following commands.

## Install the setup
```
    ddev composer install
    ddev drush si
    ddev drush en l10n_server l10n_drupal_rest l10n_pconfig potx queue_ui devel webprofiler
```

## Configure the setup
```
    echo '$settings["config_sync_directory"] = "../config/sync";' >> web/sites/default/settings.php
    
    ddev drush cset system.site name 'Translations'
    ddev drush cset system.site page.front '/l10n-server-project/1'
    ddev drush cim --partial
```

## Scan Drupal project and releases
```
    ddev drush l10n_server:scan
```

## Parse Drupal releases
```
    ddev drush l10n_server:parse 'Drupal core' --release='9.4.1'
``` 
    or all releases
```
    ddev drush l10n_server:parse 'Drupal core'
```

## Update the setup
```
    ddev composer update
    ddev drush updb
    ddev drush en l10n_server l10n_drupal_rest l10n_pconfig potx queue_ui devel webprofiler
```
