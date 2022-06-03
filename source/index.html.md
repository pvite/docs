---
title: Legalbox API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

# toc_footers:
#   - <a href='#'>Sign Up for a Developer Key</a>


includes:
  - errors

search: false

code_clipboard: false

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Scraper API

> Base URL: https://api.legalbox.cl/

```
200 - OK.
400 - Bad Request: Likely due to an invalid or missing parameter.
401 - Unauthorized.
404 - Not Found.
429 - Too many requests, too quickly.
```

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.



# Authentication

## Token

Incluir el Token para cada endpoint con el siguiente formato:

`curl -H 'Authorization: {token}' https://api.legalbox.cl/`


<aside class="notice">
Todas las request deben tener 
</aside>


# Requests

## Crear una nueva request


```shell
curl "https://api.legalbox.cl/v1/s/requests/?tipo=juridico&rut=60450260k" \
  -H "Authorization: AUTH_TOKEN"
```

> Response

```json
{
  "status_code": 200,
  "request_id": "d4f0d7f0-79f2-49c0-845c-a92b67c8995a",
  "message": "request created",
}
```

Los parámetros 'nombre', 'apellido_paterno', 'apellido_materno' no son necesarios si el 'tipo' de persona es jurídica.


### HTTP Request

`POST https://api.legalbox.cl/v1/s/requests`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
tipo | (string) | Tipo de persona (natural / juridica)
rut | (string) | R.U.T de la persona
nombre | (string) | Nombre de la persona natural
apellido_paterno | (string) | Apellido paterno de la persona natural
apellido_materno | (string) | Apellido materno de la persona natural

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a specific Request

```shell
curl "https://api.legalbox.cl/v1/s/requests/d4f0d7f0-79f2-49c0-845c-a92b67c8995a" \
  -H "Authorization: AUTH_TOKEN"
```

> Response

```json
{
    "request_id": "d4f0d7f0-79f2-49c0-845c-a92b67c8995a",
    "created_at": 1654029037,
    "params": {
      "tipo": "juridico",
      "rut": "93307000k",
    },
    "status": "done",
    "result": [

    ],
    "time": 1320
}
```

This endpoint retrieves a specific Request information.

### HTTP Request

`GET https://api.legalbox.cl/v1/s/requests/<REQUEST_ID>`

### URL Parameters

Parameter | Type | Description
--------- | ------ | -----------
REQUEST_ID | (string) | ID de la Request


## Get all the Requests

```shell
curl "https://api.legalbox.cl/api/kittens/2" \
  -H "Authorization: AUTH_TOKEN"
```

> Response

```json
[
  {
    "request_id": "d4f0d7f0-79f2-49c0-845c-a92b67c8995a",
    "created_at": 1654029037,
    "params": {
      "tipo": "juridico",
      "rut": "93307000",
      "dv": "k"
    },
    "status": "done",
    "result": [

    ],
    "time": 1200
  },
  {
    "request_id": "68cef817-84d1-4ac1-a9fa-d660d6f12dff",
    "created_at": 1654029037,
    "params": {
      "tipo": "natural",
      "rut": "10947306",
      "dv": "5",
      "nombre": "Perico",
      "apellido_paterno": "Gonzalez",
      "apellido_materno": "Perez"
    },
    "status": "done",
    "result": [

    ],
    "time": 945
  }
]

```

This endpoint retrieves all the requests made.


### HTTP Request

`GET https://api.legalbox.cl/v1/s/requests`


### Response

Parameter | Type | Description
--------- | ------ | -----------
request_id | (string) | ID de la Request
created_at | (integer) | Fecha creación de la Request
status | (string) | Estado de la Request
tipo | (string) | Tipo de persona
rut | (string) | R.U.T de la persona
dv | (string) | Dígito verificador de la persona
nombre | (string) | Nombre de la persona natural
apellido_paterno | (string) | Apellido paterno de la persona natural
apellido_materno | (string) | Apellido materno de la persona natural
time | (integer) | Duración de la Request en segundos




