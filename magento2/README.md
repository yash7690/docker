
	docker compose build

	docker compose up -d

	docker exec -it ce245_php bash

	cd projects/ce245

	composer create-project --repository=https://repo.magento.com/ magento/project-community-edition=2.x.x .

	php bin/magento sampledata:deploy

	php bin/magento setup:install \
		--base-url=http://{version}.localhost.com/ \
		--backend-frontname=admin \
		--db-host=db --db-name={dbname} --db-user=root --db-password=root \
		--admin-firstname={FirstName} --admin-lastname={LastName} --admin-email={email} \
		--admin-user=admin --admin-password=admin123 --language=en_US \
		--elasticsearch-host=elasticsearch \
		--currency=USD --timezone=America/Chicago --use-rewrites=1