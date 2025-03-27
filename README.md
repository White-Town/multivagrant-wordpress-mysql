# Vagrant Multi-VM Setup for WordPress and MySQL

## Overview

This repository provides a comprehensive setup for creating a multi-VM environment using Vagrant. The environment consists of two virtual machines:

- **Web VM**: Hosts an Apache server with WordPress installed.
- **Database VM**: Runs MySQL to store WordPress data.

The VMs are configured to communicate over a private network, allowing WordPress to seamlessly connect to the MySQL database.

## Requirements

Before proceeding, ensure the following software is installed on your machine:

- **[Vagrant](https://www.vagrantup.com/)** (Version 2.2.0 or higher)
- **[VirtualBox](https://www.virtualbox.org/)** (or another supported provider)

## Setup Instructions

Follow these steps to set up and run the multi-VM environment.

### 1. Clone the Repository

Clone this repository to your local machine:

```bash
git@github.com:White-Town/multivagrant-wordpress-mysql.git
cd multivagrant-wordpress-mysql
```

### 2. Project Structure

After cloning, the project structure should look like this:

``` bash

multivagrant-wordpress-mysql/
│── Vagrantfile                   # Main Vagrant configuration file
│── scripts/
│   ├── common.sh                 # Common provisioning script for all VMs
│   ├── web.sh                    # Web server setup script (Apache + WordPress)
│   ├── db.sh                     # Database setup script (MySQL)
│── web_files/                    # Directory for files to sync with the web server VM
│── db_files/                     # Directory for files to sync with the database server VM

```

### 3. Start the Virtual Machines

Navigate to the project directory and start the VMs:
 ``` bash
    cd multivagrant-wordpress-mysql
    vagrant up
```
This command will provision both the Web VM and the Database VM.

### 4. Accessing the Setup

Once the VMs are up and running, you can access the services as follows:

    WordPress: Open http://192.168.56.6 in your web browser.
    
        Username: wordpress-user

        Password: password

### 5. Stopping & Destroying VMs

- To stop the VMs:
``` bash

vagrant halt
```

- To completely remove the VMs:
``` bash
vagrant destroy -f
```

### 6. Troubleshooting

Web Server Issues: If the web server fails to start, re-run the provisioning script for the Web VM:

``` bash
    vagrant provision web
```
Change the bind address. Got the given file and set bind address to 0.0.0.0
cd /etc/mysql/mysql.conf.d/mysqld.cnf
- bind-address		= 0.0.0.0
Go to this directory and change the document root to
- DocumentRoot /srv/www/wordpress

And add this file below document root
```bash
    <Directory /srv/www/wordpress>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>


```
One more thing to do is go this directory and add 
- vim /etc/mysql/my.cnf
  ```bash
  [mysqld]
   bind-address = 0.0.0.0
  ```

MySQL Access Issues: If MySQL is not accessible, check the firewall settings on the Database VM:

```bash
    sudo ufw status
```    

### Conclusion

This Vagrant setup provides a isolated environment for developing and testing WordPress applications with a dedicated MySQL database. Enjoy your development experience!

### License

This project is licensed under the MIT License.

### Contribution

Feel free to fork this repository and submit pull requests.
### Reference
- https://gist.github.com/rmatil/8d21620c11039a442964


Thank You ..
