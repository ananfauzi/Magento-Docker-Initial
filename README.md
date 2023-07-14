# Magento-Docker-Initial
This repo contain docker compose configuration for installing magento 2.4.x <br />
Before use this repository docker and docker-compose is required to be installed on your system's. <br />
<br />
<br />
Here step by step, magento installation after cloning this repository: <br />
1. build n run all the containers
```
docker compose up -d --build
```
2. execute bash inside web container
```
docker compose exec web bash
```
3. download magento files via composer
```
sudo composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .
```
download can't run automatically, you need to fill the credentials. Please see <a href="https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html#">here</a>, to get the credentials. <br />
4. Install magento
```
bin/magento setup:install \
--base-url=http://localhost:5000 \
--db-host=db \
--db-name=magento \
--db-user=admin \
--db-password=password \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=admin@example.com \
--admin-user=admin \
--admin-password=admin123 \
--language=en_US \
--timezone=America/New_York \
--use-rewrites=1 \
--elasticsearch-host=elastic \
--elasticsearch-port=9200 \
--earch-engine=elasticsearch7
```
5. Install sample data (optional)
```
bin/magento sampledata:deploy
bin/magento setup:upgrade
bin/magento indexer:reindex
bin/magento cache:flush
```
6. Run the installation
```
php -S 0.0.0.0:5000 -t ./pub/ ./phpserver/router.php
```
open your browser on http://localhost:5000
