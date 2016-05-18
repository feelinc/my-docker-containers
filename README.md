#My Docker containers collection

Rename docker-compose-example.yml file into docker-compose.yml, then edit anything you desired.

Build using below command :
docker-compose up --build

Run as daemon using below command :
docker-compose up -d

Stop :
docker-compose stop

You can switch to use PHP-FPM or HHVM in nginx/site.conf, choose between hhvm.conf or php-fpm.conf

You can also switch the PHP-FPM version.