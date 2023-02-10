# Idenfy Magento demo store

## Prerequisites
- A working [DDEV installation](https://ddev.readthedocs.io/en/stable/)
- Magento [Authentication keys](https://devdocs.magento.com/guides/v2.4/install-gde/prereq/connect-auth.html)

## Installation
To setup this demo store locally please follow the following steps

### 1. Starting your ddev instance
Start your DDEV instance using the following command:
```shell
ddev start
```

### 2. SSH Key authentication
Add ssh key authentication to the ddev-ssh-auth container so you can access repo's using your host SSH key:
```shell
ddev auth ssh
```

### 3. Installing Magento
First retrieve all required packages:
```shell
ddev composer install
```

Next install your magento instance:
```shell
ddev magento setup:install \
--base-url=https://idenfy.ddev.site \
--db-host=db \
--db-name=db \
--db-user=db \
--db-password=db \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=admin@admin.com \
--admin-user=admin \
--admin-password=AdminUser123! \
--language=en_US \
--currency=USD \
--timezone=Europe/London \
--use-rewrites=1 \
--search-engine=elasticsearch7 \
--elasticsearch-host=elasticsearch \
--elasticsearch-port=9200 \
--elasticsearch-index-prefix=idenfy_magento \
--elasticsearch-timeout=15
```

### 4. Installing sample data
Deploy the default Magneto sample data:
```shell
ddev magento sampledata:deploy
```

Run the setup upgrade command to make sure all your data is up to date
```shell
ddev magento setup:upgrade
```

Run the reindexing process
```shell
ddev magento index:reindex
```

Flush all Magento caches`
```shell
ddev magento cache:flush
```

### 5. Visit the demo store
You should now be able to access your demo store on https://idenfy.ddev.site/
