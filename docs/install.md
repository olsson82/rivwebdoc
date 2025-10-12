# Install Rivendell Web Broadcast

![Screenshot](img/install.png)

The installation of the system is simple, but before you install your system, you need to have all the requirements for your server.

!!! Info

    **This guide is for Debian based system**

## Install Dependencies

### Apache

Normally apache is installed during installation of Rivendell, but if not, you need to install it with following command:

```
sudo apt install apache2 -y
```

### mod_rewrite

To be able to use the system you need apache modrewrite installed. This is done by enable the apache module:

```
sudo a2enmod rewrite
```

Then you need to make changes in your apache config to allow .htaccess files:

Open up config file : 
```
sudo nano /etc/apache2/apache2.conf
```

Go and make sure that directory /var/www is set to **AllowOverride All**

### PHP

This is developed to work with PHP version 8 but will work on version 7 also.

Install php with following:

```
sudo apt install php php-{common,mysql,xml,xmlrpc,curl,gd,imagick,cli,dev,imap,mbstring,opcache,soap,zip,intl,pdo} -y
```

This will install PHP and modules that are common and needed.

Also make some adjustments in php.ini file that you will find in /etc/php/8.2/apache2 folder (replace 8.2 with the version number for your php)

Some suggestions:

| Setting      | Value |
| ----------- | ----------- |
| max_execution_time      | 180       |
| memory_limit   | 128M        |
| post_max_size   | 200M        |
| upload_max_filesize   | 200M        |
| max_input_time   | 60        |
| max_input_vars   | 3000        |

If you have problems load audio files or upload, you need to adjust these more.

Now restart apache:
```
 sudo systemctl restart apache2
```

### FFMPEG

For the moment we use FFMPEG to get the length of the audio files, this will be removed in the future, but for now you need to install FFMPEG on your server:

```
sudo apt install ffmpeg
```

## Install System

Now we are going to install the system on your server. This must be done on a server that has Rivendell installed.

Start by login to root user: 
```
su -l
```

Go to apache folder: 
```
cd /var/www/html
```
and remove the index file: 
```
rm index.html
```

### Stable versions

A release file is "more stable" than the "github" code, when we update the version number we release a new release. This can contain less bugs, than clone the github code. And we recommend this way. For future releases you can just use the built in updater, and it will install new updates automatic for you.

<a href="https://github.com/olsson82/rivendellweb/releases/latest" target="_blank">Download the latests release</a> select the tar.gz file and download it to /var/www/html folder.

To download direct to html folder use wget:

```
wget https://url-to-latest-tar.gzfile
```

then extract it with following:
```
tar --strip-components=1 -zxf rivendellweb-0.6.4.tar.gz
```
Change the rivendellweb-0.6.4.tar.gz to correct file, then remove the tar.gz package with:
```
rm rivendellweb-0.6.4.tar.gz
```
### Development versions

If you want the latest changes in the system, Clone the github repository inside the html folder. 

Do it with following when you are in the html folder:
```
git clone https://github.com/olsson82/rivendellweb.git .
```
Don't forget the last dot!

!!! Warning

    **This is the development and changes a lot and can hold many bugs!**

### Read & Write

The updater need read and write access to the server to update the system on new releases.

### Reverse Proxy

It's recommended that you use reverse proxy with https access before you expose the machine on the world wide web. For testing you can use http://localhost

Audio recording needs https access to work, but they will work on localhost also.

I will not go in to detail on this part but one i can recommend is to use Cloudflare and Nginx Proxy Manager.

## Run the installer

Open up Rivendell Web Broadcast in your browser.

### Pre check
![Screenshot](img/precheck.png)

The installation will first check your system to see that the most important parts is correct on your server. If everything looks good, you can continue, if it's not good, there will be a red warning on that part. Fix that and reload the page to start installation by pressing the next button that will be available.  

### Admin user

Under the admin user field you enter your or anyones username on rivendell with normal user access on rivendell. This user will get admin access to the web system. 

!!! Info

    **Rivendells Admin user can not be used in this system**

Just enter one username now, you can add more later.

### SMTP Settings

The SMTP settings are used to send out emails in the system and is required.

## Updates

In the admin dashboard you will get information when a new release is avaliable. Read the Updates part for more info about the update section.

## Cron job for log generation

If you are going to use the log generation part you need to setup cron job that runs every minute.

First make shure you have curl installed on your server:

```
apt install curl -y
```

Login as root

```
su -l
```
and go in to crontab with 
```
crontab -e
```

Add the following to the crontab:

```
* * * * * curl -s http://localhost/api/generator.php > /dev/null
```

## Cron job for backups

The system can make backups automatic on Rivendell MySQL database and also on Rivendell Web Broadcast data files. To do so you need to setup a cron job on you server.

First make shure you have curl installed on your server:

```
apt install curl -y
```

Login as root

```
su -l
```
and go in to crontab with 
```
crontab -e
```

Add for example following to do backup each midnight:

```
0 0 * * * curl -s http://localhost/api/backup.php > /dev/null
```

