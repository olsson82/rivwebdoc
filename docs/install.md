# Install Rivendell Web Broadcast

![Screenshot](img/install.png)

The installation of the system is simple, but before you install your system, you need to have all the requirements for your server.

For the moment there are no server check in the installer so you need to do this process first.

**This guide is for Debian based system**

## Install Dependencies

### Apache

Normally apache is installed during installation of Rivendell, but if not, you need to install it with following command:

`sudo apt install apache2 -y`

### mod_rewrite

To be able to use the system you need apache modrewrite installed. This is done by enable the apache module:

`sudo a2enmod rewrite`

Then you need to make changes in your apache config to allow .htaccess files:

Open up config file : `sudo nano /etc/apache2/apache2.conf`

Go and make sure that directory /var/www is set to **AllowOverride All**

### PHP

This is developed to work with PHP version 8 but will work on version 7 also.

Install php with following:

`sudo apt install php php-{common,mysql,xml,xmlrpc,curl,gd,imagick,cli,dev,imap,mbstring,opcache,soap,zip,intl,pdo} -y`

This will install PHP and modules that are common and needed.

Now restart apache: `sudo systemctl restart apache2`

### FFMPEG

For the moment we use FFMPEG to get the length of the audio files, this will be removed in the future, but for now you need to install FFMPEG on your server:

`sudo apt install ffmpeg`

## Install System

Now we are going to install the system on your server. This must be done on a server that has rivendell installed.

Start by login to root user: `su -l`

Go to apache folder: `cd /var/www/html` and remove the index file: `rm index.html`

### Stable versions

A release file is "more stable" than the "github" code, when we update the version number we release a new release. This can contain less bugs, than clone the github code. And we recommend this way.

Download the latests release and extract it inside the /var/www/html folder.

### Development versions

If you want the latest changes in the system, Clone the github repository inside the html folder. **This is the development and changes a lot and can hold many bugs!**

### Data Folder

Chmod the data folder so it get read and write access. This folder store json settings files for the system, logeditor and password reset.

### Reverse Proxy

It's recommended that you use reverse proxy with https access before you expose the machine on the world wide web. For testing you can use http://localhost

Audio recording needs https access to work, but they will work on localhost also.

## Run the installer

Open up Rivendell Web Broadcast on your browser to start installation. You will have to fill out some important settings first. All settings can be changed later in the system.

### Admin user

Under the admin user field you enter your or anyones username on rivendell with normal user access on rivendell. This user will get admin access to the web system. **Rivendells Admin user can not be used in this system**

Just enter one username now, you can add more later.

### SMTP Settings

The SMTP settings are used to send out emails in the system and is required.

## Updates

In the admin dashboard you will get information when a new release is avalible, This will only inform when there are new release on the release page on github.

To update just replace all files with the new updated, clear your catche and if needed there can be an update guide.

