---
parent: For developers
nav_order: 20
---

# Installation guide

{: .important }
> * This installation guide always references to the [latest stable version]({{site.repo_url}}/releases).
> * If you want to update your installation to another version, read the [migration guide]({{ site.baseurl }}/en/migration-guide).
> * You can help making this open source project more visible on GitHub by starring ⭐ it.

## Requirements
* Server with **shell access** and **cronjobs**
* [Webserver - Nginx or Apache]({{ site.baseurl }}/en/webserver-configuration.html)
* PHP => 8.2 (prior to v3.6 PHP 8.1)
* PHP intl extension INTL_ICU_VERSION >= 50.1
* PHP bzip2 lib (for automatic database backups) (prior to v3.6: PHP ZipArchive class)
* MySQL >= 8.0
* If you cloned the repository from Github: Node.js, npm >= v7 and Composer v2

{: .note }
> * There is an offer for [paid support and hosting](https://www.foodcoopshop.com/das-angebot/) if you don't want to spend your time on IT stuff.
> * There are demo installations in [German](https://demo-de.foodcoopshop.com/) and [English](https://demo-en.foodcoopshop.com/). Feel free to test before installing.

* * *

## 1) [Setting up your dev environment **with Docker**]({{site.baseurl }}/en/docker-dev-environment)

## 2) Setting up your dev environment **without Docker**

{: .important }
We strongly recommend using our docker dev environment.

* If you want to set up a dev environment, clone from Github.
* After that, you need to manually install composer and npm vendors.
* The main branch always equals the latest stable version provided on [https://www.foodcoopshop.com/download](https://www.foodcoopshop.com/download).
* The only difference is, that the zip file already includes the vendors which were already installed by the following commands):
```
$ composer install
$ npm --prefix ./webroot install ./webroot
```
* So run that commands if you cloned from Github.
* Don't forget to change app.debug to true in your custom_config.php.

## 3) Installing the latest stable version for your live server
* Download the latest stable version at [https://www.foodcoopshop.com/download](https://www.foodcoopshop.com/download) and upload the unpacked files to your server using FTP.
* [Webserver configuration]({{ site.baseurl }}/en/webserver-configuration.html)

## Setting permissions
```
bash ./devtools/installation/set-permissions.sh
```

{: .new }
If you install a version prior to v3.6, [run the commands in this file]({{site.repo_url}}/blob/develop/devtools/installation/set-permissions.sh).

* * *

## Configuration
* Copy [custom_config.default.php]({{site.repo_url}}/blob/main/config/custom_config.default.php) to custom_config.php and add your configuration overrides.
* The default configuration is found in [app_config.php]({{site.repo_url}}/blob/main/config/app_config.php).
* Set `app.cakeServerName` to your server, e.g. "https://yourdomain.tld" - NO TRAILING SLASH!

{: .new }
> * `app.cakeServerName` was changed to `App.fullBaseUrl`

* Some configuration is stored in the database and can easily be changed from the admin area: https://yourdomain.tld/admin/configurations (Super Admin account required)
* [More infos]({{ site.baseurl }}/en/settings)

## Database Setup
* Create a new database (e.g. foodcoopshop_db)
* Define your database configuration in custom_config.php

{: .important-title }
> <= v3.5
> * At first, **import the [initial database structure]({{site.repo_url}}/blob/main/config/sql/_installation/clean-db-structure.sql)**
> * Then **import initial database data in [German]({{site.repo_url}}/blob/main/config/sql/_installation/clean-db-data-de_DE.sql) or [English]({{site.repo_url}}/blob/main/config/sql/_installation/clean-db-data-en_US.sql)**. You can't easily change the language after the installation.

{: .new }
> * run `bash ./devtools/installation/init-database.sh de_DE` (locale "en_US" is also supported)
> * Import taxes for Austria: `bash ./bin/cake migrations seed --seed AddTaxesAustriaSeed`
> * **OR** Import taxes for Germany: `bash ./bin/cake migrations seed --seed AddTaxesGermanySeed`


## Credentials
* Copy [credentials.default.php]({{site.repo_url}}/blob/main/config/credentials.default.php) to credentials.php and change the configuration
* The email error logging can be enabled to ease server monitoring
* **Be aware** that you need to set `'EmailTransport' => [...]` twice, once in `credentials.php` and once in `custom_config.php`. There must be an EmailTransport config-block for the keys "default" and "debug" so the configs must not stay commented!
* See [https://book.cakephp.org/4/en/core-libraries/email.html#configuring-transports](https://book.cakephp.org/4/en/core-libraries/email.html#configuring-transports)

## Testing your email configuration
* Once you created a Super Admin account (instructions further down), You can test your email configuration by accessing https://yourdomain.tld/admin/configurations/sendTestEmail in your browser.

## Setup security keys
Open your domain https://yourdomain.tld in a browser and follow the steps shown to create secure values for the security salt ```Security.salt```. Set it in custom_config.php

## Create the valid Super Admin account
* Open https://yourdomain.tld/sign-in in your browser and register with your personal email address (down below at "Create account")
* After the successful registration go to your database (e.g. using Adminer or phpMyAdmin) and open the table "fcs_customer". There is one record (with your email address). Change the field "id_default_group" from 3 to 5 and  the field "active" from 0 to 1.
* Open https://yourdomain.tld/request-new-password, type in your email address and press "Send".
* With the password that was sent to you by email you are able to login as a Super Admin.

{: .important }
> The urls in this section depend on the locale of your installation and therefore may be different for you. The urls are constructed from translatio -settings which can be found in the "/resources/locale/country_CULTURE/default.po" file under the keys "route_sign_in" and "route_request_new_password". Example for "de_DE":
> * Sign-in: https://yourdomain.tld/anmelden
> * Request-new-password: https://yourdomain.tld/neues-passwort-anfordern

## Setting up cronjobs
Follow the steps of the [cronjob documentation]({{ site.baseurl }}/en/cronjobs).

## Customizing CSS
* Change app.debug to `true` in your custom_config.php so that the assets (css and js) are loaded from the actual files in /css and /js (and not from /cache).
* To re-build the assets in /cache for production, run `composer build`

{: .important }
If you downloaded the package with installed vendors from foodcoopshop.com/download, you get a "Missing Plugin DebugKit" exception when you turn app.debug to true. If you can't install composer on your server, download the package from https://github.com/cakephp/debug_kit and copy it into the plugins folder. [More Details](https://github.com/foodcoopshop/foodcoopshop/issues/931).

{: .note }
Good luck and thank you for using FoodCoopShop!

## If you have questions, first check existing github support issues
* [I#519]({{site.repo_url}}/issues/519), [I#509]({{site.repo_url}}/issues/509), [I#466]({{site.repo_url}}/issues/466)
* If you still have questions, [create a new issue]({{site.repo_url}}/issues/new).
