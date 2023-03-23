# Modern WP Setup

This is a setup with:

- [Bedrock](https://github.com/roots/bedrock)
- [Acorn](https://github.com/roots/acorn)
- [SQLite](https://github.com/aaemnnosttv/wp-sqlite-db)

The goal is to have a modern WordPress setup using [Bedrock](https://github.com/roots/bedrock) as the base. This installation also uses [SQLite](https://github.com/aaemnnosttv/wp-sqlite-db) instead of the standard MySQL to keep it low profile.

## Deploying

This repo also includes the `docker` folder which includes files needed to run this project in docker. It is quite opinionated and the documentation is rather lacking because this is mostly for personal use.

## Notes/Caveats

PHP-FPM is run as root because it's a headache to deal with.
