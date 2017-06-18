# glpi-sdk-python

[![Build Status](https://travis-ci.org/truly-systems/glpi-sdk-python.svg?branch=master)](https://travis-ci.org/truly-systems/glpi-sdk-python)
![PyPi version](https://img.shields.io/pypi/v/glpi.svg)


GLPI SDK written in Python.

## Description

This SDK is written in Python to help developers integrate their apps, APIS and scripts in GLPI infrastructure. This SDK abstract
the [GLPI Rest API](https://github.com/glpi-project/glpi/blob/9.1/bugfixes/apirest.md).

To usage it, you should have username, password and API-Token from your GLPI server.

To create an API token: Setup > General > API :
* `Enable Rest API` : `Yes`

See also:
* [GLPI Rest API](https://github.com/glpi-project/glpi/blob/9.1/bugfixes/apirest.md#glpi-rest-api--documentation)


## Install

Just install from:

* PyPi:

  ```bash
  pip install glpi
  ```

* repository (development):

  ```bash
  pip install -e git+https://github.com/truly-systems/glpi-sdk-python.git@master#egg=glpi
  ```

* requirements.txt (development)

    ```shell
    pip install -r requirements-dev.txt
    ```

## Usage

You should enable the GLPI API and generate an App Token.

Please, export these environments variables with yours config:

  ```bash
  export username = "GLPI_USER"
  export password = "GLPI_USER"
  export url = 'http://glpi.example.com/apirest.php'
  export glpi_app_token = "GLPI_API_TOKEN"
  ```

Then import it in your script and create a `glpi` API connection:

  ```python
  import os
  from glpi import GLPI

  url = os.getenv("GLPI_API_URL") or None
  user = os.getenv("GLPI_USERNAME") or None
  password = os.getenv("GLPI_PASSWORD") or None
  token = os.getenv("GLPI_APP_TOKEN") or None

  glpi = GLPI(url, token, (user, password))
  ```

To usage the SDK, you just set the DBTM item that you want and get information from GLPI.

The Item value must be valid, otherwise you will get the following error.

```shell
[
    "ERROR_RESOURCE_NOT_FOUND_NOR_COMMONDBTM",
    "resource not found or not an instance of CommonDBTM; view documentation in your browser at http://<GLPI_URL>/apirest.php/#ERROR_RESOURCE_NOT_FOUND_NOR_COMMONDBTM"
]
```

### Get all Tickets

  ```python
  print "Getting all Tickets: "
  print json.dumps(glpi.get_all('ticket'),
                    indent=4,
                    separators=(',', ': '),
                    sort_keys=True)
  ```

### Create an Ticket

  ```python

  ticket_payload = {
    'name': 'New ticket from SDK',
    'content': '>>>> Content of ticket created by SDK API <<<'
  }

  ticket_dict = glpi.create('ticket', ticket_payload)
  if isinstance(ticket_dict, dict):
    print "The ticket request was sent. See results: "

  print json.dumps(ticket_dict,
                    indent=4,
                    separators=(',', ': '),
                    sort_keys=True)
  ```

### Get ticket by ID

  ```python
  print "Getting Ticket with ID 1: "
  print json.dumps(glpi.get('ticket', 1),
                    indent=4,
                    separators=(',', ': '),
                    sort_keys=True)
  ```

### Profile information

  ```python
  print "Getting 'My' profile: "
  print json.dumps(glpi.get('getMyProfiles'),
                    indent=4,
                    separators=(',', ': '),
                    sort_keys=True)
  ```

### Location

  ```python
  print "Getting 'Locations': "
  print json.dumps(glpi.get('location'),
                    indent=4,
                    separators=(',', ': '),
                    sort_keys=True)
  ```

### Full example

> TODO: create an full example with various Items available in GLPI Rest API.


## CONTRIBUTING

See [CONTRIBUTING.md](CONTRIBUTING.md)
