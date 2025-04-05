# Quick Start for Drupal 11 and Lando

**RETIRED!** This repository is no longer maintained. Please refer to the [Binbiriz Quick start for Drupal core using Lando](https://github.com/Binbiriz/lando-drupal-core-quick-start) repository.

**Requirements:** [Lando](https://lando.dev/).

All of the bash commands in this document must be run in repo root.

After cloning the repo, you're free to delete the `.git` directory.

```bash
rm -rf ./.git/
```

## Prepare Code base

```bash
lando start
```

After starting Lando, you will see the URLs. Please do not visit them at this moment.

![Lando Start URLs](https://i.imgur.com/X7ioisD.png)

Continue running the command below:

```bash
lando composer create-project drupal/recommended-project /app/temp --no-install

rsync -rtv --remove-source-files ./temp/ ./drupal/

find ./temp -type d -empty -delete # or run `rm -rf ./temp/`

rm ./drupal/web/.gitkeep

lando composer install # do not forget to confirm plugins when prompted
```

Install drush

```bash
lando composer require "drush/drush"

# Test drush
lando drush --version
```

## Install Site

### Manual Installation via Browser

You can now visit the URLs mentioned above and perform an installation via browser:

![Manual Drupal Installation](https://i.imgur.com/jxMDLac.png)

### Automated Installation via drush

#### Standard Drupal Installation

This will perform a standard Drupal installation:

```bash
# Ref: https://drushcommands.com/drush-9x/site/site:install/
# drush si --db-url=mysql://root:pass@localhost:port/dbname
lando drush site-install \
  standard \
  --site-name='Drupal using Lando' \
  --locale=en \
  --db-url=mysql://drupal11:drupal11@database:3306/drupal11 \
  --account-name=admin \
  --account-pass=admin \
  --yes
```

![Standard Drupal Installation Home Page](https://i.imgur.com/7Kyh31D.png)

#### Standard Drupal Installation in Another Language

If you want to perform a standard Drupal installation with a different language, change the `locale` option (in this example `tr` (Turkish) is used):

```bash
# Ref: https://drushcommands.com/drush-9x/site/site:install/
# drush si --db-url=mysql://root:pass@localhost:port/dbname
lando drush site-install \
  standard \
  --site-name='Drupal using Lando' \
  --locale=tr \
  --db-url=mysql://drupal11:drupal11@database:3306/drupal11 \
  --account-name=admin \
  --account-pass=admin \
  --yes
```

![Standard Drupal Installation in Another Language Home Page](https://i.imgur.com/wG8D0CD.png)

#### Install Umami Demo Profile

This is a multi-lingual Drupal demo containing realistic content:

```bash
# Ref: https://drushcommands.com/drush-9x/site/site:install/
# drush si --db-url=mysql://root:pass@localhost:port/dbname
lando drush site-install \
  demo_umami \
  --site-name='Umami Food Magazine' \
  --db-url=mysql://drupal11:drupal11@database:3306/drupal11 \
  --account-name=admin \
  --account-pass=admin \
  --yes
```

![Drupal Umami Food Magazine Demo Home Page](https://i.imgur.com/dI648Dz.jpeg)

## Admin Interface

Visit [https://dev-drupalcore.lndo.site/user/login](https://dev-drupalcore.lndo.site/user/login).

If 'Automated Installation via drush' is used for installation, use `admin` for both username and password.

![Drupal Login Page](https://i.imgur.com/PT9DdIx.png)
