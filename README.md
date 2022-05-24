# Simplifier docker-compose template
Docker-Compose templates to run [Simplifier](https://simplifier.io)

## simplifier-standalone.yml
Single Simplifier Instance with corresponding MySQL and Reverse Proxy Traefik

##  Quick Setup Guide
edit .env file (SIMPLIFIER_HOSTNAME, leave other variables at the default value)
copy server certificats to /etc/simplifier/traefik
copy security.toml to /etc/simplifier/traefik
edit security.toml to match your needs, at least change name of certificate files

## Environment Variables
### SIMPLIFIER_HOSTNAME
Insert a valid dns name for example 'example.simplifier.cloud'.

> :warning: Use a valid dns name for the Variable HOSTNAME - IP Adresses won't work for HOSTNAME because Traefik don't like this.
> If you are not capable to generate a valid dns with certificate, just modify your host file (for e.g. /etc/hosts) and flush your dns cache

### DB_PASSWORD
Password of the database user 'simplifier'

### DB_NAME
Name of the database schema. Should be 'appserver', leave it as is.

### DB_ROOT_PASSWORD
Root password of the root user. Should be 'root' by default, unless you have changed it manually.

### SIMPLIFIER_VERSION
Define the Simplifier runtime version. 

### SIMPLIFIER_DATA_VOL
Define the data directory for simplifier. Default is '/opt/simplifier/data', unless you have changed it. 

> :warning: We assume that you have mounted the database storage directory under '${SIMPLIFIER_DATA_VOL}/mysql'. If that is not the case
> please reach out to us.

## Installation Manual

1. Clone Branch 'update-onpremise-image'

`git clone --branch update-onpremise-image https://github.com/simplifier-ag/docker-compose.git`

Prepare Directories for Docker Volumes on your host

2. Modify Variables in .env File

Adjust Hostname and if needed Simplifier Version, leave other variables at their default, unless you have manually changed something. 
*See section "Environment Variables"*

3. Create Certificate Volume for TLS Certfificates

`mkdir -p /etc/simplifier/traefik` 

4. Optional - Add TLS Certficates (if you haven't any, Traefik will generate default ones)

copy your certificates to /etc/simplifier/traefik

copy and edit security configuration
`cp security.toml /etc/simplifier/traefik/`
`nano /etc/simplifier/traefik/security.toml`

5. Run Simplifier

`docker-compose -f simplifier-standalone.yml up -d && docker-compose -f simplifier-standalone.yml logs -f`

Press Strg+X if no error occurs in the logs

6. Open Hostname with your Browser

https://yourHostname/UserInterface

7. Insert your License Key

8. Login with admin/admin
... and change your admin and guest user password

9. Download Marketplace Content and import it (Menu -> Transport)

[Download here](https://community.simplifier.io/marketplace/standard-content/)

10. Register on our [Community Page](https://community.simplifier.io/)

and learn how to use Simpifier in our [free online courses](https://community.simplifier.io/courses/)!
