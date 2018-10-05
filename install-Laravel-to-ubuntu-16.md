We are going to install Laravel and all the associated components making use of the Terminal commands. If you would like to gain a better understanding of all the commands we use throughout this tutorial or would just like a handy cheat sheet you can refer to, too help remember all the commands and their uses.

 Linux & Ubuntu Terminal Command Cheat sheets

In order to proceed with the installation process open a terminal window or use ctrl + alt + t which will open a terminal window for you.

How to install PHP 7.2 on Ubuntu 16.04
The first requirement is the PHP and a few additional PHP components. If you are going to only want to leverage the convenience of Homestead, you can skip this step, as Homestead comes with PHP and all the required components already installed. However, as a PHP developer, you will probably want PHP on your development machine for convenience sake and the ability test and develop other PHP based solutions.

It’s always good practice to update your repositories and carry out any upgrades.
```
sudo apt update && sudo apt upgrade -y
```
At the time of writing this post is PHP 7.2, is not included in the default Official Ubuntu repositories for Ubuntu 16.04. However, PHP 7.2 will be included in Ubuntu 17.10 & 18.04.

Check out our guide to installing PHP 7.2 and Laravel on Ubuntu 18.04

To install PHP 7.2 on ubuntu 16.04 we will need to add a link to an alternate repository to gain access to the installation files.

First in order to do so we will also need to install a package that will allow you to easily manage your distribution and independent software vendor sources.

sudo apt-get install software-properties-common
Once installed we can add a link to the new repository and update
```
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
```
We can now go ahead and install PHP 7.2 with all the additional components we need.
```
sudo apt install php7.2 php7.2-cli php7.2-common php7.2-json php7.2-opcache php7.2-mysql php7.2-mbstring php7.2-zip php7.2-fpm php7.2-xml -y
```
To ensure we have everything installed and PHP is working lets quickly check the version using php -v

php version check

How to install MySQL on Ubuntu 16.04
You can install whichever database server you wish but in my case I needed to use mysql
```
sudo apt install mysql-server
```
Once installed just you’ll want to run the included security script. This changes some of the less secure default options for things like remote root logins and sample users.
```
mysql_secure_installation
```
How to install curl on Ubuntu 16.04
Typically on fresh installs of ubuntu cURL is not installed. cURL is a computer software project providing a library and command-line tool for transferring data using various protocols.

sudo apt install curl
How to install Composer on Ubuntu 16.04
The Laravel uses the composer to manage your dependencies, so the next step is to installComposer.
```
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
```
Change permissions on composer so you can run it without sudo
```
sudo chown -R $USER ~/.composer/
```
How to install Symfony on Ubuntu 16.04
Laravel leverages another PHP framework, Symfony, quite intensively so it worthwhile installing Symfony on your development machine too.

We’ll use Composer to install the Skeleton and create a test project , cunningly called testproj

composer create-project symfony/skeleton testproj
Afer installing and creating the test projects lets run it to check we have everything working as expected.

Symfony install 

Lets quickly run the project to test all is working. Change into the directory cd testproj and execute php -S 127.0.0.1:8000 -t public

We can now open our browser and navigate to: http://localhost:8000/

We should see the test page which confirms all is up and running


We’re now ready to install Laravel using composer
```
composer global require "laravel/installer"
```
All that is left to do now is ensure Laravel is added to your PATH. You can open your ~/.bashrc and paste the line below
```sh
export PATH="$HOME/.composer/vendor/bin:$PATH"
```
or if you’re feeling ambitious and you have backed up your current,~/.bashrc you can attempt this line to do it all in one line
```
echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >> ~/.bashrc
```
All we now need to do is refresh the bash profile because we have made changes
```
source ~/.bashrc
```
How to Start a Laravel project on Ubuntu 16.04
We’re all set now to create a project using Laravel. We can use either method of starting a project i.e. using Laravel commands of composer based. For the purpose of this guide, we’ll be using Laravel.

To start a new project create a directory you would like to store your projects i.e. mkdir projects

change into the directory – cd projects – then we can use the Laravel command to create a new project which in this instance is a simple To Do List web application we’ll name notepad, but you can name it whatever you choose.

composer create-project --prefer-dist laravel/laravel notepad

Once the application is generated we can cd notepad the php artisan serve and we then open a browser and visit http://localhost:8000 we’ll see the Laravel sample page

Laravel Test Page



 

How to install Homestead on Ubuntu 16.04
At this stage we have the Laravel framework installed and we are able to generate projects. However, to truly enjoy the benefits of Laravel we should install the Homestead environment.

What is Homestead
Laravel Homestead is a pre-packaged virtual machine that provides development environment without requiring you to install PHP, a web server, and any other server software on your local machine. You don’t have to worry about messing up your operating system!

Homestead makes use of Technology called Vagrant, that enables users to create and configure lightweight, reproducible, and portable development environments. Vagrant boxes are completely disposable. If something goes wrong, you can destroy and re-create the box in minutes!

In order to make use of Vagrant,  we need to install both Virtual Box and Vagrant.

Install VirtualBox
VirtualBox is a cross-platform virtualization application. What does that mean? For one thing, it installs on your existing Intel or AMD-based computers, whether they are running Windows, Mac, Linux or Solaris operating systems.

It’s free and available from Oracle VM VirtualBox

Don’t install Virtualbox from the default 16.04 Repositories as this is an out of date version of Virtualbox – Virtualbox 5.2.x is the latest.

To install virtual box and the Virtual box extension pack which adds useful new features to this popular virtualisation package.

# Add a link to the new repository
```
sudo sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian xenial contrib" >> /etc/apt/sources.list.d/virtualbox.list'
```
# Set up key ring trusts to the new repository

```
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -

wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
```
## Update 
```
sudo apt-get update
```
## Install
```
sudo apt-get install virtualbox-5.2
```
At the time of writing this post, there seemed to be an issue with installing the virtual box extension pack via the terminal, so I needed to use a work-around.

Download Virtual Box Extension pack 5.2.10 and manually install it.

Once the download  completes,  Open Virtualbox and install the extension pack: 
File -> Preferences -> Extensions -> Adds new package (“+” Button)

Install Vagrant
Vagrant provides a simple and easy to use command-line client for managing these environments, and an interpreter for the text-based definitions of what each environment looks like, called Vagrantfiles.

Don’t install the version of Vagrant available in the default repositories for Ubuntu 16.04 because it is an old version and will not work with the latest release of homestrad
```
wget https://releases.hashicorp.com/vagrant/2.1.0/vagrant_2.1.0_x86_64.deb
sudo dpkg -i vagrant_2.1.0_x86_64.deb
```
## Check the version 
vagrant version
Once vagrant is installed we can add the laravel/homestead box. This process usually takes about 13-20 minutes depending on your internet connection and spec of your machine.

You will only ever need to do this one when setting up your machine initially.

vagrant box add laravel/homestead

You will be asked which provider you would like to use choose VirtualBox and proceed. Once this is complete we are now ready to configure homestead on a per project basis.

Configure Homestead Per Project
Homestead is configured using a YAML file, which contains configuration information regarding sites & files on your computer, databases to create etc. When you start a new project, you have to add an entry to this file and re-provision.

When using Homestead on a per-project basis, you keep this file with your project and it contains only that project’s settings. Enabling you to quickly clone a project if it’s under source control, and quickly boot a Homestead instance for that project.

This is especially helpful when setting an existing project up on a new computer, as you don’t need to manually set up Homestead and configure it for your project.

To create a Homestead.yaml for your project, first, we need to add Laravel/Homestead development dependency to our project.

To do this cd into your project directory then execute

composer require laravel/homestead --dev
Once complete we can now use this package to initialise files Homestead will require and create the Homestead.yaml
php vendor/bin/homestead make

If you check your directory now you will notice a Homestead.yaml file has been created.
```yaml
ip: 192.168.10.10
memory: 2048
cpus: 1
provider: virtualbox
authorize: ~/.ssh/id_rsa.pub
keys:
    - ~/.ssh/id_rsa
folders:
    -
        map: /home/gary/code/testsource
        to: /home/vagrant/code/testsource 
sites:
    -
        map: testsource.test
        to: /home/vagrant/code/testsource/public
databases:
    - homestead
```    
    
name: testsource
hostname: testsource
We are now almost ready to run our project, all we need to do now is add an entry to our Host file for the website.

sudo gedit /etc/hosts


Then we add an entry for our new website and save the file
192.168.10.10 sourcelink.test
if you’re confident enough you can also do the above using the following command
echo "192.168.10.10 testsource.test" | sudo tee -a /etc/hosts

We can now just execute vagrant up and browse to the test site http://sourcelink.test
