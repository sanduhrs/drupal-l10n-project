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
    echo '$settings["config_sync_directory"] = "../config/sync";' >> web/sites/default/settings.php
    ddev drush si --existing-config
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

## Import content entities
```
    ddev drush en default_content l10n_server_default_content
    ddev drush pmu default_content l10n_server_default_content
```

## Update the setup
```
    git pull
    ddev composer update
    ddev drush updb
    ddev drush en l10n_server l10n_drupal_rest l10n_pconfig potx queue_ui devel webprofiler
```

## Theme development

Bluecheese is based on ruby / compass / susy ...
To install system dependencies see http://compass-style.org/install/

```
    cd web/themes/contrib/bluecheese
    bundle install
```
if you are using ruby >= 3.0.0
```
    cd web/themes/contrib/bluecheese
    bundle add sorted_set
    bundle install
```
Compile the CSS, once
```
    bundle exec compass compile
```
Compile the CSS, continously
```
    bundle exec compass watch .
```
