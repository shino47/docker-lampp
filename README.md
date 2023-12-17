# docker-lampp

Development environment with:

* Debian
* Apache
* MariaDB
* PHP
* phpMyAdmin
* Mailpit

PHP included in this bundle uses the [PHP](https://hub.docker.com/_/php/) image with Apache tag,
which also uses the [Debian](https://hub.docker.com/_/debian) image.

## Virtual hosts

By default, the Apache containers defines a volume on `/etc/apache2/sites-enabled`, so you can add
configuration files in the `volumes/apache-php*` directories to define virtual hosts. For example,
you can create a file named `sites.conf` with the following:

```xml
<VirtualHost *:80>
  DocumentRoot "/var/www/html/foo"
  ServerName foo.local
</VirtualHost>

<VirtualHost *:80>
  DocumentRoot "/var/www/html/bar"
  ServerName bar.local
</VirtualHost>
```

Now, you have to edit your `/etc/hosts` file and add:

```
127.0.0.1    foo.local
127.0.0.1    bar.local
```

## Laravel

The Apache containers uses the default `bridge` network mode. So, if you want to execute database
`artisan` commands in the host, you will receive errors because of the connection.

You can edit the `.env` file and change the `DB_HOST` variable to:

```ini
DB_HOST=172.17.0.1
```

`172.17.0.1` is the default host IP in the bridged network. Basically, you are connecting from the
Laravel app to the host's database.

### Mailpit

To use Mailpit in a Laravel application, you can edit your `.env` file:

```ini
MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_ENCRYPTION=null
MAIL_USERNAME=no-reply@example.com
MAIL_PASSWORD=null
```

Is not mandatory to set the encryption nor the password.

Again, if you need to execute `artisan` commands that requires send emails, you will need to change
the `MAIL_HOST` to the host IP in the bridged network:

```ini
MAIL_HOST=172.17.0.1
```
