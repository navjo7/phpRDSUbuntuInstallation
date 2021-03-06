﻿# PHP with RDS installation on UBUNTU

PHP with RDS installation on UBUNTU

## Getting Started

These instructions contains commands to install php and RDS on your ec2 ubuntu

### Prerequisites

Create an EC2 instance and RDS instance on AWS

## Installation

open ec2 ubuntu using putty

run the below commands

1. `sudo su`

1. `apt-get update`

1. `apt-get upgrade -y`

1. `apt-get dist-upgrade -y`

1. `apt-get autoremove -y`

1. `apt-get install apache2 php7.0 php7.0-cli php7.0-fpm php7.0-gd php-ssh2 libapache2-mod-php7.0 php7.0-mcrypt mysql-server php7.0-mysql git unzip zip postfix php7.0-curl mailutils php7.0-json phpmyadmin -y`

1. `phpenmod mcrypt`

1. open file `nano /etc/apache2/sites-enabled/000-default.conf`

    * add line at top of the file : `Include /etc/phpmyadmin/apache.conf`

    * then `ctl+o` to save and `ctl+x` to exit

1. restart server `service apache2 restart`

1. `nano /etc/phpmyadmin/config.inc.php`
    * scroll down untill you see a line `/* Authentication type */`

    * just before this line paste : 

```
    $i++;
    $cfg['Servers'][$i]['host']          = '__FILL_IN_DETAILS__';
    $cfg['Servers'][$i]['port']          = '3306';
    $cfg['Servers'][$i]['socket']        = '';
    $cfg['Servers'][$i]['connect_type']  = 'tcp';
    $cfg['Servers'][$i]['extension']     = 'mysql';
    $cfg['Servers'][$i]['compress']      = FALSE;
    $cfg['Servers'][$i]['auth_type']     = 'config';
    $cfg['Servers'][$i]['user']          = '__FILL_IN_DETAILS__';
    $cfg['Servers'][$i]['password']      = '__FILL_IN_DETAILS__';
```

* replace `__FILL_IN_DETAILS__` with details from your RDS

1. To change owner of your folders `sudo chown -R ubuntu:ubuntu /var/www/html/`

# Enable `mail()` function of php on ubuntu

1. Run the below commands on instance
* `sudo apt-get install sendmail`
* `sudo sendmailconfig`
* `sudo service apache2 restart`


# Install AWS sdk on PHP

1. Run the below commands on instance
* `curl -sS https://getcomposer.org/installer | php`
* `php composer.phar require aws/aws-sdk-php`


## Authors

* **Navjot** - [Website]


## License

This project is licensed under the MIT Privacy Policy - see our [Privacy and Policies] file for details

## Acknowledgments

* None
