# ojs3-docker

## Description

This repository offers a fully dockerized version of [PKP's](https://pkp.sfu.ca/) OJS 3 in addition to a set of DAI specific plugins.

## Usage

### Git submodules

Initialize submodules by running

    git submodule update --init --recursive
    

### OJS SQL dump

The repository provides the SQL dump of a minimal installation. To use the minimal setup see the [README](mariadb_data/README.md). Alternatively you can your own  SQL dump into [mariadb_data](mariadb_data) instead of using the [mariadb_data/init.sql_template](mariadb_data/init.sql_template).
    
### .env file
Copy the .env-default template 

    cp .env-default .env

and customize its contents. If you use the default init.sql, you should be ready to go without any changes.


### Docker

Managing the image is done by docker-compose.

Build the image with

    docker-compose build

Start the container with

    docker-compose up

Stop the container by terminating the process (ctrl+C) or using

    docker-compose stop
    
Destroy all existing containers (including all changes to mariadb) with

    docker-compose down -v
    
## XDebug

The repo is configured for using xdebug. However, one needs to make the appropriate settings inside one's own ide. Dependig on which type one is using, this differ a little. 

### VSCode

If you don't have a lunch.json
Click on Debug -> Start debugging. In the opening popup choose php as option. 
Now you have a autogenerated lunch.json, the countend should look like this.
You need to add the pathMappings, and adjust the path to your lokal folder.

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "port": 9000,
            "pathMappings": {
                "/var/www/html": "/path/to/workspace/ojs"
            }
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 9000
        }
    ]
}
```

Now you can start a debug session. Navigate to the debug tab on the right side of your screen and hit the small run symbol in your upper part of the righthand column.

A small overlay with a play, stop and other buttons should open.

## License

Licensed under GPL-3.0. For further information see LICENSE.
