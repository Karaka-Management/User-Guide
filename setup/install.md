# Installation

The easiest and most common way to install the application is through the web installer. Alternatively you can also install it through a command line interface (cli).

* Server Recommendations
* Webserver and Database
* Php
* Software
* Application Instllation

## Server Recommendations

The server recommendations strongly depend on your individual needs, in the following you will find some general recommendations.

| Type             | Minimum requirements                   | Recommendations                                                           |
| :--------------- | :------------------------------------- | :------------------------------------------------------------------------ |
| Storage          | SSD 1 GB +space for documents          | SSD 10 GB +space for documents                                            |
| CPU              | i5 3.2 GHz / Xeon E3 3.8 GHz (4 cores) | Xeon Silver 2.40 GHz (10 cores) min. 4 cores dedicated to the application |
| RAM              | 4GB DDR3 3000 MHz                      | 32 GB DDR4 3200                                                           |
| Operating System | Linux or Windows                       | Linux                                                                     |

> The above mentioned recommendations are for the basic application use case without additional tools and software which you maybe want to install or have already running on the server. Furthermore, the amount of concurrent users also impacts which hardware requirements are necessary (above we calculated with 50 concurrent users)

## Web server and Database

If you don't have a web server already installed please install the web server of your choice. Web servers which are supported are apache2 and nginx. Databases which are supported are mysql/mariadb, postgres and mssql/sqlsrv.

### Windows

If you are on Windows you may want to download and install the newest version of [Xampp](https://www.apachefriends.org/download.html) / [Bitnami](https://bitnami.com/stack/wamp). During the installation please make sure your install `php` and `mysql`.

### Linux

On linux you may want to install `apache2` and `mysql`. Please note you can also use this application with `nginx` and `postgres`:

```sh
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update

sudo apt-get install software-properties-common apache2 mysql-server

sudo a2enmod rewrite
sudo a2enmod headers
```

## Php

The minimum php version requirement in the following installation guide is version 8.0.

### Windows

On Windows php should already be installed with the web servers mentioned above just like the various extensions.

### Linux

The following extensions are recommended and sometimes even mandatory:

```sh
sudo apt-get install php8.1 php8.1-dev php8.1-cli php8.1-common php8.1-mysql php8.1-pgsql php8.1-xdebug php8.1-opcache php8.1-pdo php8.1-sqlite php8.1-mbstring php8.1-curl php8.1-imap php8.1-bcmath php8.1-zip php8.1-dom php8.1-xml php8.1-phar php8.1-gd php-pear sqlite3
```

## Software

### Mandatory

#### OCR

Some modules in the application may need text recognition of scanned files (e.g. DocumentManagement). If you don't use such a module you don't need to install this.

##### Windows

Download and install [tesseract-ocr](https://tesseract-ocr.github.io/tessdoc/Downloads.html).
Download and install [pdftotext](https://www.xpdfreader.com/pdftotext-man.html).
Download and install [pdftoppm](https://www.xpdfreader.com/pdftoppm-man.html).

##### Linux

```sh
sudo apt-get install tesseract-ocr poppler-utils
```

### Optional

#### Caching

Caching allows the application to store data in memory instead of re-calculating it again and again. This can speed up the general behavior of the application. Supported caching are redis and memcached (**not** memcache)

##### Windows

On windows you may want to download and install [redis](https://redis.io/download).

##### Linux

For caching you may install redis or memcached:

```sh
sudo apt install redis-server
sudo phpenmod redis
```

## Application Installation

### Files

Before you can install the application you need to put the application files into the web server directory. This directory depends on the web server which you used and the web server configuration.

#### Windows

By default the windows directory should be `C:/xampp/htdocs`. Remove all files in this directory and put all the files of the Karaka application into this directory.

#### Linux

By default the linux directory should be `/var/www/htm`. Remove all files in this directory and put all the files of the Karaka application into this directory.

### Web Installer

If you installed the application on your local computer you can open a browser window and navigate to [http://127.0.0.1/Install](http://127.0.0.1/Install). If you installed it on a remote server navigate to the URL of that server.

Click yourself through the installation and fill out the forms during the installation process.

#### Pre-installation check

On the page called pre-installation check the installation script will check and inform you if the necessary php extensions and file permissions are available. Only requirements marked as optional can be missing. If any other requirements fail please don't continue with the installation and fix these requirements first. Once you fixed the requirements reload the installation script!

##### File permissions

File permissions should only be an issue on linux. You can change the file permissions of directories as follows:

```sh
sudo chmod -R 755 /var/www/htm/Modules
```

##### Php extensions

If the extension is already installed you can just add it to your `php.ini` file of extension loading files in `conf.d/`. e.g.:

```ini
extension=mbstring.dll // Example in case you are installing on Windows
extension=mbstring.so // Example in case you are installing on Linux
```

> The `php.ini` file can be **often** found at C:/xampp/php/php.ini on Windows and /etc/php/8.0/apache2/php.ini on Linux.
>
> Sometimes the ending .dll and .so must be omitted depending on the version and configuration of your php installation.

If the extension is not installed and not activated you can alternatively run the following commands on Linux (just as example):

```sh
sudo apt-get install php8.1-mbstring
sudo phpenmod mbstring
```

On windows you may follow the php [installation guide](https://www.php.net/manual/en/install.pecl.windows.php) or the installation guide of your chosen web server which maybe already includes php.

#### Database

On this page you must enter the database information which the application can use to store data.

##### Address

The address for the database server usually is `127.0.0.1`

##### Type

The database type depends on which database you used. If you followed this installation you probably used `mysql`

##### Port

The port depends on the database you installed. Different database vendors use different ports. If you followed this installation you probably used mysql, in this case the port is `3306`. If you used another database, please check the documentation of that database to find the default port.

##### Database

The recommended database name is `oms`. Please note that this database must be manually created by you. If you've not already done so during the database installation process, please create that database now. In order to create this database please check the documentation of your database vendor. On windows you might be able to log into `phpmyadmin` and create this database.

##### Users

For security purposes we recommend that you create 5 different users in your database application who only have access to `oms` database and each one of the users may only have the following permissions. The application installation script cannot create these users, please make sure you already created them:

* One user may only be able to do schema changes
* One user may only create data
* One user may only read/select data
* One user may only update/modify data
* One user may only delete/remove data

It is possible to always input the same user and same password for all users in the installation script but this is not recommended. If you just want to get started you may input the user and password which you defined during the database installation. Nevertheless, please change this in the future.

#### Configuration

On the last page you can define the name of your organization/company.

##### Admin Login, Password, Email

Here you must define the admin login name, the admin password and email.

##### Top Level domain

The top level domain is the domain name where you installed the application. If you only installed it locally, it is 127.0.0.1. If you installed it on your web server, then you input the domain name e.g. `karaka.app`

##### Web Subdirectory

The web subdirectory by default is `/`. If you installed the application in a subdirectory instead of the main directory of your web server you input the name of the subdirectory here e.g. `/subdir/`.

#### Install

After clicking install you will either receive a message that something went wrong e.g. some configurations are wrong (please fix them) or the installation will redirect you to the login if everything went smoothly. Please make sure to delete the `Install` directory so that no-one else can use it.
