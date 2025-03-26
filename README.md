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
git clone https://github.com/yourusername/your-repo-name.git
cd your-repo-name
```

### 2. Project Structure

After cloning, the project structure should look like this:

``` bash

project-folder/
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
    cd project-directory
    vagrant up
```

This command will provision both the Web VM and the Database VM.

### 4. Accessing the Setup

Once the VMs are up and running, you can access the services as follows:
   MySQL: Connect to the database at 192.168.56.7 using the credentials:

  Username: wpuser

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
Thank You
