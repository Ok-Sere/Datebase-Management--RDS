# Datebase Management with Amazon RDS

> Project Brief

GatoGrowFast is a fast-growing IT service company that provides software development, cloud solutions, and cyber security service to businessess. With an increasing number of clients and projects, the company needs a strong and reliable database to handle all its date.  

This includes keeping track of client details, managing projects information, and processing service orders. 
As the business keeps expanding, the amount of data is getting bigger and more complex, so they need a database system that can keep up.

> ## Project Aim

This project is aimed at helping GatoGrowFast Manage its expanding data needs with a reliable database solution.

To achieve this we will be setting up and managing database using Amazon RDS to help handle client data and project information effectively.

> ## Step 1 - Creating Database

### Configuration 
- The first step is to navigate to the RDS Service on the AWS consol, and create a DataBase.

![Database](./img/1.%20database.png)

- We will be using the *Standard database* creation method, and *MySQL* engine type to help us store and manage information in an organized way. 

![Database](./img/2.%20settings.png)

- Engine version *MySQL 8.0.40* and free tier template will be used.

![Database](./img/3.%20config.png)

- The DB instance identifier is named as *'My-rds-Database'*, and the credential management is set as *'self managed'*.

![Database](./img/4.%20config%202.png)

- DB instance class is configured as *db.t3.micro*,
- A VPC is attached as well as a security group that permits inbound traffic on port 3306. 


![Database](./img/5.%20VPC%20&%20SG.png)

The database instance must covers at least two Availability Zones, to achieve this, another subnet was added in additional availability zone.

The new subnet was added to the DataBase Subnet Group in the RDS settings.

- After configuring the Database settings, we were able to create an available database.

![Database](./img/6.%20result.png)


> ## Step 2 - Launch EC2

- The next step is to create an EC2 instance and attach the same security group we attched to our database.

- We will be using SSH to connect to out EC2 instance.

- Next we will be using command `sudo wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm`to download the repository package for MySQL YUM repository. This allows the installation of MySQL server and related tools.

![EC2](./img/9.%20AWS.png)


- Once the file has been downloaded, we will install the package and configure the system to use the official MySQL repositor using command `sudo yum localinstall mysql57-community-release-el7-11.noarch.rpm`

![EC2](./img/10%20AWS.png)

- We will now be importing the GPG Key using command `sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022`. This step ensures that any MySQL packages we download and install is verified.

This step is important because When using yum to install packages from the MySQL repository, your system checks if the packages are signed with a trusted GPG key. By importing this key, you enable the verification process, ensuring the packages are secure and legitimate.

- We will now be installing MySQL database server on our Amazon linux EC2 instance using command `sudo yum install mysql-community-server`. This enables the instance to host and manage MySQL Databases.

![EC2](./img/12.sudo%20yum%20install.png)

- Using command `sudo systemctl start mysqld`, we will be starting the MySQL service and allowing the service interact with the database hosted on the server.

- Command `sudo systemctl enable mysqld` will enable the MySQL service to start automatically when the system boots up for convinience. With this command, we don't need to start the MySQL server manually everytime we restart the instance.

- To display the current status of the MySQL service we will use command `sudo systemctl status mysqld`. Currently the MySQL service is active and running as seen below.

![EC2](./img/13%20ec2.png)

> ## Step 3 - Connect RDS to EC2 instance 

- To connect RDS to Ec2, we will be executing command `mysql -h my-rds-database.ctyykuys07nw.eu-west-2.rds.amazonaws.com -u your-username -p`. This cammand is made up of our client programme `mysql`, the endpoint of the database server using flag `-h my-rds-database.ctyykuys07nw.eu-west-2.rds.amazonaws.com`, username for our database created when setting up the RDS Instance `-u admin`, and the password for this specific username.

- To view all databases, we will simply type in 'SHOW DATABASES' on the terminal.
To use the database we have created, we will type in 'USE mysql'.
![EC2](./img/14.%20SHOW%20DATA%20BASESES%20AND%20MYSQL.png)

- To show tables inside the database, we will type in 'SHOW TABLE' on the terminal.

![EC2](./img/15%20SHOW%20TABLES%20.png)


>## OUTCOME

After using Amazon RDS with MySQL, GatoGrowFast will now be able to handle growing data needs effectivly. This setup provides the scalability, security, and reliability needed to support the expansion of the company.