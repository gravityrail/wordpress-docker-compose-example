# Sample configuration for developing WordPress locally

Based on two blog posts ([part 1](http://goldsounds.com/archives/2015/04/06/quick-and-easy-wordpress-development-using-docker/), [part 2](http://goldsounds.com/archives/2015/04/16/docker-for-wordpress-multisite-development/)) describing how to use Docker for WordPress plugin, theme and MultiSite development.

## Instructions

Install [Docker](https://docs.docker.com/installation/) and [Docker Compose](http://docs.docker.com/compose/install/), then:

```bash
git clone https://github.com/gravityrail/wordpress-docker-compose-example.git
cd wordpress-docker-compose-example
docker-compose up
```

You'll see a bunch of output from the running processes - nginx, php-fpm and mysql.

On OS X, open a new Terminal window and enter:

```bash
open "http://$(boot2docker ip):8080"
```

If everything worked correctly, you should see the installer for your WordPress web site!

You should also see a `src` directory within the git repo which contains the latest version of WordPress. You can edit this code, unzip plugins and themes and customize to your heart's content and all the changes will show up instantly when you reload the URL in your browser.

## Scripting the container

As an added bonus, which container adds the `wp` command from the [wp-cli](http://wp-cli.org) project. This allows you to modify your WordPress site from the command line.

To run this from outside the container, you can use "docker-compose run" like this:

```bash
docker-compose run wordpress wp --allow-root plugin install hello-dolly
```

This is a bit verbose, so you may want to create this alias and save it in your `~/.profile`

```bash
alias docker-wp='docker-compose run wordpress wp --allow-root'
```

Which turns the command above into:

```bash
docker-wp plugin install hello-dolly
```

Cool, right? Want to create a new plugin but tired of writing all that scaffolding? Now just run:

```bash
docker-wp scaffold plugin my_super_plugin --plugin_name="My Super Plugin"
```