# docker-lampp

Development environment with:

* Debian
* Apache
* MariaDB
* PHP 7
* PHP 5
* phpMyAdmin

PHP included in this bundle uses the [php](https://hub.docker.com/_/php/) image with apache tag,
which also uses the [debian](https://hub.docker.com/_/debian) image.

This bundle includes both, PHP 7 and PHP 5, so you can work in projects with different version at
the same time.

## Virtual hosts

By default, the Apache containers defines a volume on `/etc/apache2/sites-enabled`, so you can add
configuration files to define virtual hosts. For example, you can add a file named `sites.conf` with
the following:

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

The Apache containers uses the default `bridge` network mode. So, if you want to execute `artisan`
commands in the host, you will receive errors because of the database connection.

One solution is to log into the container a execute the commands in there.

You can also, edit the `.env` file and change the `DB_HOST` variable to:

```ini
DB_HOST=172.17.0.1
```

`172.17.0.1` is the default host IP in the bridged network. Basically, you are connecting from the
Laravel app to the host's database.
