We are going to install Laravel and all the associated components making use of the Terminal commands. If you would like to gain a better understanding of all the commands we use throughout this tutorial or would just like a handy cheat sheet you can refer to, too help remember all the commands and their uses.

 Linux & Ubuntu Terminal Command Cheat sheets

In order to proceed with the installation process open a terminal window or use ctrl + alt + t which will open a terminal window for you.

How to install PHP 7.2 on Ubuntu 16.04
The first requirement is the PHP and a few additional PHP components. If you are going to only want to leverage the convenience of Homestead, you can skip this step, as Homestead comes with PHP and all the required components already installed. However, as a PHP developer, you will probably want PHP on your development machine for convenience sake and the ability test and develop other PHP based solutions.

It’s always good practice to update your repositories and carry out any upgrades.

sudo apt update && sudo apt upgrade -y
At the time of writing this post is PHP 7.2, is not included in the default Official Ubuntu repositories for Ubuntu 16.04. However, PHP 7.2 will be included in Ubuntu 17.10 & 18.04.

Check out our guide to installing PHP 7.2 and Laravel on Ubuntu 18.04

To install PHP 7.2 on ubuntu 16.04 we will need to add a link to an alternate repository to gain access to the installation files.

First in order to do so we will also need to install a package that will allow you to easily manage your distribution and independent software vendor sources.

sudo apt-get install software-properties-common
Once installed we can add a link to the new repository and update

sudo add-apt-repository ppa:ondrej/php

sudo apt-get update

We can now go ahead and install PHP 7.2 with all the additional components we need.

sudo apt install php7.2 php7.2-cli php7.2-common php7.2-json php7.2-opcache php7.2-mysql php7.2-mbstring php7.2-zip php7.2-fpm php7.2-xml -y
To ensure we have everything installed and PHP is working lets quickly check the version using php -v

php version check

How to install MySQL on Ubuntu 16.04
You can install whichever database server you wish but in my case I needed to use mysql

sudo apt install mysql-server
Once installed just you’ll want to run the included security script. This changes some of the less secure default options for things like remote root logins and sample users.

mysql_secure_installation
How to install curl on Ubuntu 16.04
Typically on fresh installs of ubuntu cURL is not installed. cURL is a computer software project providing a library and command-line tool for transferring data using various protocols.

sudo apt install curl
How to install Composer on Ubuntu 16.04
The Laravel uses the composer to manage your dependencies, so the next step is to installComposer.

curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
Change permissions on composer so you can run it without sudo

sudo chown -R $USER ~/.composer/
How to install Symfony on Ubuntu 16.04
Laravel leverages another PHP framework, Symfony, quite intensively so it worthwhile installing Symfony on your development machine too.

We’ll use Composer to install the Skeleton and create a test project , cunningly called testproj

composer create-project symfony/skeleton testproj
Afer installing and creating the test projects lets run it to check we have everything working as expected.

Symfony install 

Lets quickly run the project to test all is working. Change into the directory cd testproj and execute php -S 127.0.0.1:8000 -t public

We can now open our browser and navigate to: http://localhost:8000/

We should see the test page which confirms all is up and running
