# Gardening

pre-packaged Vagrant box that provides you a wonderful development environment  
without requiring you to install PHP(7.0), HHVM(3.15), a web server(Nginx or Apache),  
and any other server software on your local machine.

php7 box:
```json
"require-dev": {
  "ytake/gardening": "~0.0"
}
```

(supported for virtualbox only)

## boxes
https://atlas.hashicorp.com/ytake

## Included Software
 - CentOS 7
 - Git
 - PHP 7.x (remi repository)
 - Apache (2.4.6)
 - Nginx (1.12)
 - MySQL (5.7)
 - Sqlite3
 - PostgreSQL (9.5)
 - Composer (1.5)
 - Node.js (Gulp, webpack)
 - Redis(4.0)
 - Memcached
 - Elasticsearch(5.6)
 - Kibana(5.6)
 - MongoDB
 - Java(1.8)
 - fluentd
 - Couchbase(4.5)

## included php extensions

```
[PHP Modules]
amqp
apc
apcu
ast
bcmath
bz2
calendar
cassandra
Core
couchbase
ctype
curl
date
dom
event
exif
fileinfo
filter
ftp
gd
gettext
hash
iconv
igbinary
imagick
json
ldap
libxml
mbstring
mcrypt
memcached
mongodb
msgpack
mysqli
mysqlnd
openssl
pcntl
pcre
pcs
PDO
pdo_dblib
pdo_mysql
pdo_pgsql
pdo_sqlite
pdo_sqlsrv
pgsql
phalcon
Phar
phpiredis
posix
rdkafka
readline
redis
Reflection
session
shmop
SimpleXML
soap
sockets
SPL
sqlite3
sqlsrv
standard
Stomp
sysvmsg
sysvsem
sysvshm
tokenizer
uopz
uuid
wddx
xdebug
xhprof
xml
xmlreader
xmlwriter
xsl
Zend OPcache
zip
zlib
zmq

[Zend Modules]
Xdebug
Zend OPcache
```

## Composer global
included:
 - friendsofphp/php-cs-fixer
 - squizlabs/php_codesniffer
 - phpmd/phpmd

## MySQL and PostgreSQL
 - user: gardening
 - password: 00:secreT,@

## Xdebug
default:
```
xdebug.remote_enable = 1
xdebug.remote_connect_back = 1
xdebug.remote_port = 9080
xdebug.max_nesting_level = 512
xdebug.idekey = PHPSTORM
```

## Install Gardening Box

### case 1, your "home" directory
```bash
$ cd ~
$ git clone https://github.com/ytake/gardening.git gardening
```

setup.sh(Windows .bat) command from the gardening directory to create the vagrant.yaml configuration file.(~/.gardening hidden directory)

```bash
$ bash setup.sh
```

### case2, Per Project Installation

To install gardening directly into your project, require it using Composer:

```bash
$ composer require ytake/gardening --dev
```

use the make command to generate the Vagrantfile and gardening.yaml(or gardening.json) file in your project root.

```bash
$ ./vendor/bin/gardening gardening:setup
```

gardening.json:
```bash
$ ./vendor/bin/gardening gardening:setup --filetype=json
```

## Configuration

### Choose Web Server
default Nginx

```yaml
web_server: nginx
```

Apache can be selected if necessary

```yaml
web_server: httpd
```

### Configuring Shared Folders

```yaml
folders:
    - map: /path/to/yourProject
      to: /home/vagrant/yourProjectName
```

many shared folders:
```yaml
folders:
    - map: /path/to/yourProject
      to: /home/vagrant/yourProjectName
    - map: /path/to/yourSecondfProject
      to: /home/vagrant/yourSecondProjectName
```

### Configuring Sites
```yaml
sites:
    - map: gardening.app
      to: /home/vagrant/yourProject/public
```

many sites:
```yaml
sites:
    - map: gardening.app
      to: /home/vagrant/yourProject/public
    - map: gardening.second.app
      to: /home/vagrant/yourSecondProject/public
```

use symfony by setting the type option:
```yaml
sites:
    - map: gardening.app
      to: /home/vagrant/yourProject/public
      type: symfony
```

### Optional

#### Fluentd

[Fluentd](https://www.fluentd.org/)

use Fluentd by setting the fluentd option to true:

```yaml
fluentd: true
```

#### MongoDB

[MongoDB](https://www.mongodb.com/)

use MongoDB by setting the mongodb option to true:

```yaml
mongodb: true
```

#### Elasticsearch

[Elasticsearch](https://www.elastic.co) 

use Elasticsearch by setting the elasticsearch option to true:

```yaml
elasticsearch: true
```

#### Kibana

[Kibana](https://www.elastic.co/products/kibana)

use Kibana by setting the kibana option to true:

```yaml
kibana: true
```

#### Couchbase

[Couchbase](https://www.couchbase.com/)

use Couchbase by setting the couchbase option to true:

```yaml
couchbase: true
```
*Access to admin console http://vagrantIpAddress:8091*

### Ports

By default, the following ports are forwarded to your gardening environment:

 - SSH: 2222 → Forwards To 22
 - HTTP: 8000 → Forwards To 80
 - HTTPS: 44300 → Forwards To 443
 - MySQL: 33060 → Forwards To 3306
 - Postgres: 54320 → Forwards To 5432
 - MongoDB: 47017 → Forwards To 27017
 - Elasticsearch: 19200 → Forwards To 9200
 - kibana: 56010 → Forwards To 5601
 
Forwarding Additional Ports:
```yaml
ports:
    - send: 7777
      to: 777
```
