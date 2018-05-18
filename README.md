# Linux Server Configuration for Dog Breed Catalog

## Access
- **IP Address/Port:** 54.149.44.57:2200
- **URL:** http://ec2-54-149-44-57.us-west-2.compute.amazonaws.com

&nbsp;
## Software Installed
- apache2
- flask
- git
- httplib2
- libapache2-mod-wsgi
- oauth2client
- postgresql
- python-dev
- python-pip
- python-psycopg2
- requests
- sqlalchemy
- virtualenv

&nbsp;
## Configuration
- Made sure all packages were up-to-date using `apt-get update` and `apt-get upgrade`
- Updated the file `/etc/ssh/sshd_config` to do the following:
  - Change the SSH Port to 2200
  - Prevent root from logging in remotely
  - Force SSH authentication
- Updated the firewall settings
  - `sudo ufw default deny incoming`
  - `sudo ufw default allow outgoing`
  - `sudo ufw allow 2200/tcp`
  - `sudo ufw allow 80/tcp`
  - `sudo ufw allow 123/udp`
  - `sudo ufw enable`
- Added new user `grader` using `adduser`
  - Gave grader `sudo` access by adding `/etc/sudoers.d/grader`
  - Created an ssh key for grader using `ssh-keygen` (on local machine)
  - Added the public key to `home/grader/.ssh/authorized_keys` and updated permissions to the file and directory
- Updated the timezone to UTC using `dpkg-reconfigure tzdata`
- Created database and database user `catalog` and granted the user access to the database
- Cloned git repository inside of `/var/www`
- Made updates to code to work in this environment
  - Removed vagrant-related stuff
  - Updated directory structure and renamed `views.py` to `__init__.py`
  - Added `app.wsgi`
  - Updated to use PostgreSQL with the `catalog` database instead of SQLite
  - Updated paths to JSON files and upload directory
- Made sure `.git` was only accessible to owner using `chmod 700`
- Made sure `static` was accessible so uploaded dog breed images could be added (`chmod 777`)
- Created a new virtual host - `/etc/apache2/sites-available/catalog.conf`
- Updated oauth settings to allow http://ec2-54-149-44-57.us-west-2.compute.amazonaws.com/

&nbsp;
## Resources
- https://medium.com/coding-blocks/creating-user-database-and-adding-access-on-postgresql-8bfcd2f4a91e
- https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
- [Udacity Discussion Forum](https://discussions.udacity.com/c/nd004-full-stack-broadcast)
