# Enabling CI on WPEngine with GitHub and Codeship

## Create the GitHub repository

1. Create the repository on CSIS-iLab
2. It can be public or private depending on project

## Init the repository on localhost

1. Run `git init`
2. Create the WP installation
3. Keep it in your `htdocs` directory with MAMP so you can run the site locally while you develop
- Don't forget to initialize an empty database in MAMP's PHPAdmin for the install. If you're copying a WPEngine install, you'll need to reconfigure it so `wp-config.php` accesses your SQL database with root credentials and the correct database name.
4. Add this repository's `.gitignore` to the root directory of the installation
5. Add and commit your files (do not push to Git yet)

## Connect Codeship

1. Head over to www.codeship.com
2. Sign in with GitHub (I've already granted permissions for our organizational account)
3. Add the GitHub repository
4. In `Project Settings` (top right menu option with a wrench icon), you can add:
  - `Test Settings` to check code or functions should we want to implement (resource: https://pippinsplugins.com/unit-tests-wordpress-plugins-introduction/)
  - `Deployment` When you first set up, you'll want to pick a branch and then select `Custom Script` (it's the last option).

  I currently have `ci_wp_integrate` executing deploys from the `master` branch right to `production`. This is what the script looks like:

  `git remote add ci_wp_integrate git@git.wpengine.com:production/csisdc.git`

  `git push ci_wp_integrate master --force`

Where `ci_wp_integrate` is the name of the GitHub repository, and `csisdc` is the name of the WPEngine install.

This would be an unlikely arrangement during actual development. I'd suggest deploying to `staging` then using WPEngine's internal staging->production deploy system to push live changes.

## Connect WPEngine to Codeship

1. Get the SSH key from the `General` tab under `Project Settings` in Codeship
2. Copy this key into `Git push` under the WPEngine install's menu (The developer name doesn't matter)

### Profit.
