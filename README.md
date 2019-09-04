# EbookAPI Magento Plugin

## Prerequisites
- Docker-CE for development
- Git on target platform when using Github repo with Composer

## Develop
- Clone the git project
-  Bring up docker: `docker-compose up -d`
- Drop into PHP container terminal: `docker-compose exec magento bash`
- Move into container project folder: `cd /opt/bitnami/magento/htdocs/`
- [Install](#manually-copying) the component utilizing local repository, taking into consideration the the
url for the path is the one specified in the docker-compose.yml magento services volume mount-point.
By default this value is `./app/code/FourRSolutions/EbookApi/`.
- Enjoy

## Installing

### Adding Repository
There are two ways to utilize the repository: require the github repository directly,
which is preferred for third-party installations, or specifying a local directory
containing the repository files, as is to be done when developing with Docker.

#### Using Github
- Add the following to the composer.json file in the root Magento install directory:
```
 "repositories": [
        {
            "type": "vcs",
            "url":  "https://github.com/DarriusAlexander/blue360docker.git"
        }
    ]
```

#### Manually copying
- Add the following to the composer.json file in the root Magento install directory:
```
 "repositories": [
        {
            "type": "path",
            "url":  "pathToProject"
        }
    ]
```

### Requiring Module and installing
- Require module: `composer require fourrsolutions/module-ebooks-api:dev-feature/magentoPlugin`
- Install the plugin: `bin/magento setup:upgrade`
- Resolve the DI dependencies: `bin/magento setup:di:compile`

## Caveats
- If during `docker-compose up` the ElasticSearch service fails with ERROR MESSAGE
`Invalid kernel settings. Elasticsearch requires at least: vm.max_map_count = 262144`, execute this command:
`sudo sysctl -w vm.max_map_count=262144` and retry `docker-compose up`.

