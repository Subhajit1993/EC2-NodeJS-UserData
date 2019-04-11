# EC2-NodeJS-UserData
AWS EC2 instance data for Node and PM2

#!/bin/bash
exec > >(tee /var/log/user-data.log|logger -t user-data -s 2>/dev/console) 2>&1
yum update -y
yum install httpd php php-mysql -y 
yum install -y gcc make gcc-c++
yum install git -y
chkconfig httpd on
service httpd start
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
nvm install 8.9.0
npm i -g pm2
mkdir /var/www
chmod 777 -R /var/www
git clone your_repo_url /var/www/SomeFolder
chmod 777 -R /var/www/SomeFolder
cd /var/www/SomeFolder
npm install
pm2 start ecosystem.config.js  —name project_name
pm2 log
