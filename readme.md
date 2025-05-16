# Wordpress development in Docker
There may be better ways to do that ... 
(I am a noob here, but it works as intended.)

## Overview

Reproducable environment for wordpress development. 

- docker-compose.yml: PHP webserver, database server, phpmyadmin, two wordpress instances dev and prd and two dedicatet instances of wp-cli to control dev and prd. Mountpoints to interact with the local machine (Input data, configs etc.)
- prd and stg instances of Wordpress can be configured and controled by wp-cli.
  - http://localhost:8080 -> phpmyadmin
  - http://localhost:8081 -> wordpress prd
  - http://localhost:8082 -> wordpress stg

## install (basic)

- Terminal ``` docker compose up -d ``` to just run all containers. No further configurations on the wordpress instances. Call the sites with the links above.

## install (costumized)

`container-install.sh` to get the above plus a bunch of costumizations based on the files in input-data directory: 
- Enhanced file upload size
- install themes
- install plugins

## plugins.txt

This file is responsible for plugin installs - so a list of plugins get installed (not activated). 

### Must have Plugins

- create-block-theme: Quickes WP Core startup to create themes
- all-in-one-wp-migration
- theme-check: absolutly must, also if you have to make a assesement for a client's site !

### (for my tests)

- regenerate-thumbnails-advanced
- advanced-database-cleaner (currently testing this one)
- force-regenerate-thumbnails
- catch-ids
- custom-post-type-ui
- cool-timeline
- advanced-custom-fields
- display-a-meta-field-as-block

*Delete what you do not need !*

## Usage - create a new theme

Login to the dev page. 

- Dashboard->Appearance->create block theme -> create blank theme-> aktivieren
- Schriften installieren
- save the changes to your theme using Create Block Theme. The Zip should contain the theme
- eventually, copy it to the input-data directory to make it availible for the next container run or other sites.

## WPCLI Example

- `docker-compose run --user 33:33 --rm wpcli theme install <some-existing-theme-on-wordpress.org>` -> to install an online theme. Check the bash files to see what more is possible.

## Uninstall

- ``` container-uninstall.sh ``` to remove all for clean re - deploy on the same machine. 
