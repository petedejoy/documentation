---
post_title: Setting Up FTP within VPC
nav_title: Setting Up FTP within VPC
---

This is a guide for setting up an FTP server within AWS. This is useful when using an FTP Server as a source to pull files into an Astronomer Pipeline.

## Set up AWS

- New IAM role with read/write access to S3, etc
- EC2 instance
- S3 bucket.  If the bucket needs to be encrypted, follow [this guide](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html).
- PostgreSQL instance

## Set up two new domains

#### Domain for the DC/OS cluster.
This is the website that will host the dashboard for the new DC/OS cluster to be stood up within Amazon Web Services.

#### Domain for the new FTP site (i.e. ftp.somedomain.com).
This is the FTP site that authorized users can access to post files.  This should be pointed to the AWS DNS of the public agent once the cluster is created.

 ## Obtain an SSL certificate for the DC/OS cluster.
 This SSL certificate should have an RSA Key and then the certificates themselves.  The SSL certificate should be in the following format:

````
-----BEGIN RSA PRIVATE KEY-----
(Your Private Key: your_domain_name.key)
-----END RSA PRIVATE KEY-----
-----BEGIN CERTIFICATE-----
(Your Primary SSL certificate: your_domain_name.crt)
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
(Your Intermediate certificate: DigiCertCA.crt)
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
(Your Root certificate: TrustedRoot.crt)
-----END CERTIFICATE-----
````

See [this article](https://www.digicert.com/ssl-support/pem-ssl-creation.htm) for more information on creating SSL certificates.

## Obtain an SSH private key.
This is associated with the AWS Elastic Beanstalk instance.  It’s important that, when creating the cluster, this key is chosen from the drop down.

## What information is needed by Astronomer?

#### Postgres Instance

- Postgres User
- Postgres Password
- Postgres Host
- Postgres Port

#### S3 Instance

- S3 Bucket Name
- Whether the S3 bucket is encrypted

### FTP Host
- FTP Host Name (i.e. ftp.somedomain.com)
- SSL Cert
- SSH Key
- AWS_ACCESS_KEY
- AWS_SECRET_KEY
- AWS_REGION

## Generate FTP User Password
In order to add a FTP user you must generate a password hash that can be read by Astronomer's system. Contact your Implementation Specialist to obtain the password generation script.  Once obtained:
1. Navigate to the generation scripts directory with your terminal.
2. Install Node.js.
3. Run `npm install`.
4. Run `node index.js -p yourpasswordhere`.  The -p flag is optional and allows you to specify a password to be hashed, if left out the script will generate a 20 character password.  Make note of the hashed password (the long string on the line after the password that's output by the script) as well as the plain text password if you didn't choose it yourself.  The script also generates a random username you can use.

## Adding an FTP User
There are two methods that can be used to insert FTP users into Postgres, the first involves the PostgreSQL-Admin GUI tool:
1. Visit http://somedomain.com/service/postgresql-admin/ where `somedomain` is the domain of your cluster and login to DC/OS with your gmail or equivalent if not logged in.
2. If prompted to log in to phpPgAdmin, use your PostgreSQL RDS username / password.
3. We're interested in the 'ftp_users' table inside of the database name you choose for FTP.  If you can't see the schema then click 'schema' under the tree with your databases name and after putting your credentials in again you should be able to see it.
4. Click the ftp_users table and insert your username / password hash combination into the access_key_id / secret_access_key fields respectively.

Alternate method to add users:
1. Verify that you have the SSH key for your VPC instance and ssh-add it through the terminal.  (e.g. `ssh-add ~/.ssh/my_vpc_key`)
2. Run `ssh core@master_node_ip`.
3. If this is your first time adding users using this method then `docker pull postgres` to retrieve a Postgres docker image.
4. Run `docker run -d postgres` and `docker ps` again to verify that an instance of the Postgres container is live.
5. Connect to your running postgres container by running `docker exec -it your_container_id_here bash` where `your_container_id_here` is the CONTAINER ID output by `docker ps` for postgres.
6. In order to connect to your RDS Postgres run `psql -h postgres-prod.randomstring.us-east-1.rds.amazonaws.com -p your_port -U your_user_name` and then enter your password when prompted.
7. In psql run `\connect name_of_your_ftp_database` to connect to your database.
8. Run `INSERT INTO ftp_users (access_key_id, secret_access_key) VALUES ('your_username', 'your_password_hash');`.

## FAQ

### How do my users use FTP?
Download a FTP client such as [FileZilla](https://filezilla-project.org/) and to use the credentials we set above:
1. Host (e.g. `ftp.somedomain.com`)
2. Port (e.g. 10001) - set by engineering
3. Username
4. Password
5. Log in and transfer files!

### Where are files received from the FTP process stored?
Files will be synced to the S3 Bucket you create under the filepath `ftp/{username}/{files}`.

### Can users see files sent by other users?  Add files to the same root folder?
No, each user can only see their root directory `ftp/{username}` and no directory higher than that.
