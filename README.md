# Docker magento 2.4.2 starter kit

This repo is starter kit to run magento2 all setup within few commands.

## Others Information

Here i will create 3 containers to host magento2, those are defined in docker-composer.yml file
* web : This is a apache2 + php container
* mysql : This container contains maria-db version 10
* phpmyadmin : this uses apache2 server to host on port 8080 for mysql access in web browser.
* elasticsearch : elasticsearch7 

## Build and running containers
```
docker-compose up -d --build
```

### Download via composer (2.4.2:latest)
```
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.4.2 magento
```

### Localhost problem 1
```
vendor\magento\framework\Image\Adapter\Gd2.php
private function validateURLScheme(string $filename) : bool
{
	if(!file_exists($filename)) { // if file not exist
		$allowed_schemes = ['ftp', 'ftps', 'http', 'https'];
		$url = parse_url($filename);
		if ($url && isset($url['scheme']) && !in_array($url['scheme'], $allowed_schemes)) {
			return false;
		}
	}

	return true;
}
```

## Install Magento 2
```
# access your web container
docker exec -it web bash

# Navigate to web root
cd /app

#Optional but recommended: deploy sample data
php bin/magento sampledata:deploy
```
# install setup
```bash
php bin/magento setup:install --admin-firstname=John --admin-lastname=Doe --admin-email=johndoe@example.com --admin-user=admin --admin-password='Password123' --base-url=https://localhost --base-url-secure=https://localhost --backend-frontname=admin --db-host=mysql --db-name=magento --db-user=root --db-password=root --use-rewrites=1 --language=en_US --currency=USD --timezone=America/New_York --use-secure-admin=1 --admin-use-security-key=1 --session-save=files --use-sample-data --search-engine=elasticsearch7 --elasticsearch-host=elasticsearch --elasticsearch-port=9200

# elasticsearch-host=elasticsearch <container_name => `elasticsearch` >
php bin/magento setup:install --base-url=http://localhost.www/magento/magento2 --db-host=localhost --db-name=magento2 --db-user=root --db-password=root --admin-firstname=Sorabh --admin-lastname=Sharma --admin-email=ssorabh.ssharma@hotmail.com --admin-user=admin --admin-password=admin123 --language=en_US --currency=USD --timezone=America/Chicago --use-rewrites=1 --search-engine=elasticsearch7 --elasticsearch-host=localhost --elasticsearch-port=9200
```

## Disable Two factor authentication
----------------------------------
```
php bin/magento module:disable Magento_TwoFactorAuth

php bin/magento setup:static-content:deploy -f

php bin/magento indexer:reindex
```

### Unlock admin
```
php bin/magento admin:user:unlock <username>
```


