# fiware-cmd-proxy
This [flask](http://flask.pocoo.org/) application controls [ROS](http://flask.pocoo.org/) robot from a gamepad or browser.

[![TravisCI Status](https://travis-ci.org/RoboticBase/fiware-cmd-proxy.svg?branch=master)](https://travis-ci.org/RoboticBase/fiware-cmd-proxy)
[![Docker image size](https://img.shields.io/microbadger/image-size/roboticbase/fiware-cmd-proxy.svg)](https://hub.docker.com/r/roboticbase/fiware-cmd-proxy/)

## Description
This application works as a component of [FIWARE](https://www.fiware.org/).

When this application is called from [fiware orion context broker](https://catalogue-server.fiware.org/enablers/publishsubscribe-context-broker-orion-context-broker) or browser, this application extracts a 'command' from request and sends a request to orion in order to control a ROS robot.

## Requirement

**python 3.6 or higer**

## Environment Variables
This application accepts the Environment Variables like below:

|Environment Variable|Summary|Default|
|:--|:--|:--|
|`LOG_LEVEL`|log level(DEBUG, INFO, WARNING, ERRRO, CRITICAL)|INFO|
|`LISTEN_PORT`|listen port of this service|3000|
|`ORION_ENDPOINT`|endpoint url of orion context broker|http://127.0.0.1:1026|
|`PREFIX`|the prefix specified as the ambassador's annotation|''|
|`FIWARE_SERVICE`|the value of 'Fiware-Service' HTTP Header|''|
|`FIWARE_SERVICEPATH`|the value of 'Fiware-Servicepath' HTTP Header|''|
|`ROBOT_ID`|the id specified when registering robot entity to orion|''|
|`ROBOT_TYPE`|the type specified when registering robot entity to orion|''|

## Request Payload

* `/gamepad/` (application/json)

    ```json
    {
        "data": [
            {
                "button": {
                    "value": "requested_cmd",
                },
            },
        ],
    }
    ```
* `/web/` (application/x-www-form-urlencoded)

    ```text
    move=requested_cmd
    ```

## API specification

see [docs/swagger.yaml](/docs/swagger.yaml)

## Run as Docker container

1. Pull container [roboticbase/fiware-cmd-proxy](https://hub.docker.com/r/roboticbase/fiware-cmd-proxy/) from DockerHub.

    ```bash
    $ docker pull roboticbase/fiware-cmd-proxy:latest
    ```
1. Run Container.
    * Set environment variable(s) if you want to change exposed port, orion endpoint, and so on.

    ```bash
    $ env ORION_ENDPOINT="http://192.168.0.3:1026" LISTEN_PORT="3000" docker run -d -p 3000:3000 roboticbase/fiware-cmd-proxy
    ```

## Run from source code

1. start `main.py`
    * Set environment variable(s) if you want to change exposed port, orion endpoint, and so on.

    ```bash
    $ env ORION_ENDPOINT="http://192.168.0.3:1026" LISTEN_PORT="3000" docker run -d -p 3000:3000 python app/main.py
    ```

## License

[Apache License 2.0](/LICENSE)

## Copyright
Copyright (c) 2018 TIS Inc.
