# Installing DotKernel 3 `frontend`
---

# Installation

Composer is required to install DotKernel Frontend. 

### [Download Composer](https://getcomposer.org)

Instructions for installing:
* [Composer Installation -  Linux/Unix/OSX](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx)
* [Composer Installation - Windows](https://getcomposer.org/doc/00-intro.md#installation-windows)

> If you never used composer before make sure you read the [`Composer Basic Usage`](https://getcomposer.org/doc/01-basic-usage.md) section in Composer's documentation

## Choose a destination path for DotKernel 3 Frontend installation
Example:
* absolute path `/var/www/dk3`
* or relative path `dk3` (equivalent with `./dk3`)

## Installing the `frontend` Composer Package

Depending on what the purpose of your project is, one of the following packages must be installed
 * `frontend` - for web applications
 * `admin` - for administration platforms 

> Note: There is a possibility that you need both versions, in which case you must install them as different projects

### Installing DotKernel 3 Frontend

After we chose the path for DotKernel 3 (`dk` for this example) and which base package to use (`frontend` for this example) it must be installed. Therefore to install DotKernel 3 (frontend) run the following command:

```bash
$ composer create-project dotkernel/frontend -s dev /path/to/dk3
```

This command will begin by downloading the `frontend` package, after successfully downloading it the `dependencies` will be downloaded and installed.

The setup script will prompt for some custom settings. When encountering a question like the one below:

```shell
Please select which config file you wish to inject 'Zend\Session\ConfigProvider' into:
  [0] Do not inject
  [1] config/config.php
  Make your selection (default is 0):
```

For this option select `[0] Do not inject` because DotKernel 3 already has an injected config provider which already contains the prompted configurations.
If you choose `[1] config/config.php` Zend's `ConfigProvider` from `session` will be injected.

`Remember this option for other packages of the same type? (y/N)`
`YES`

The `ConfigProvider`'s can be left un-injected as the requested configurations are already loaded.


# Configuration - First Run

* import the database schema, if you are using MySQL or MariaDb, which can be found in `data/frontend.sql`
* remove the `.dist` extension of the file `local.php.dist` located in `config/autoload`
* edit `local.php` according to your dev machine. Fill in the `database` configuration and smtp credentials if you want your application to send mails on registration etc.
* get a recaptcha key pair and configure the `local.php` with them
* if you use the create-project command, after installing, the project will go into development mode automatically
* you can also toggle development mode by using the composer commands
```bash
$ composer development-enable
$ composer development-disable
```
* if not already done on installation, copy file `development.global.php.dist` to `development.global.php`

This will enable dev mode by turning debug flag to true and turning configuration caching off. It will also make sure that any previously config cache is cleared.

> Charset recommendation: utf8mb4_general_ci

# Testing (Running)


**Do not enable dev mode in production**

* Run the following command in your project's directory:

```bash
$ php -S 0.0.0.0:8080 -t public
```

> Composer's `serve` script can be used to start the PHP's built-in webserver.
> In `dotkernel3/frontend` root folder run `composer serve`
> `composer serve` will run `> php -S 0.0.0.0:8080 -t public/ public/index.php`

`0.0.0.0` means server is open to all incoming connections
`127.0.0.1` means server can only be accessed locally (localhost only)
`8080` the port on which the server is started (the listening port for the server)


* visit `http://localhost:8080` in your browser

**NOTE:**
If you are still getting exceptions or errors regarding some missing services, try running the following command
```bash
$ composer clear-config-cache
```

> If `config-cache.php` is present that config will be loaded regardless of the `ConfigAggregator::ENABLE_CACHE` in `config/autoload/zend-expressive.global.php`

Open a browser and access `http://localhost:8080/`

You should see `DotKernel Frontend` welcome page.
