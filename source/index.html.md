---
title: API Legalbox

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
    content: Documentation for the Legalbox API
---

# Input legal

> Base URL: https://api.legalbox.cl/

```
200 - OK.
400 - Bad Request: Likely due to an invalid or missing parameter.
401 - Unauthorized.
404 - Not Found.
429 - Too many requests, too quickly.
```

La API Input legal permite realizar consultas (requests), sobre personas naturales o jurídicas para obtener información de riesgo.

# Authentication

## Token

Incluir el Token para cada endpoint con el siguiente formato:

`curl -H 'Authorization: {token}' {URL}`

# Requests

## Crear una nueva request

> Example

```shell
curl -X POST "https://api.legalbox.cl/s/requests/?tipo=juridico&rut=60450260k" \
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

Al generar una Request se gatilla la búsqueda de la persona (parámetros ingresados) y se le asigna el ID que va en el response de esta request (ver ejemplo).

Este ID (request_id) es el mismo que se usa <a href="#obtener-un-request-especifico">más adelante</a> para consultar el estado de la búsqueda.



### HTTP Request

`POST https://api.legalbox.cl/s/requests`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
tipo | (string) | Tipo de persona (natural / juridica)
rut | (string) | R.U.T de la persona
nombre | (string) | Nombre de la persona natural
apellido_paterno | (string) | Apellido paterno de la persona natural
apellido_materno | (string) | Apellido materno de la persona natural

<aside class="notice">Para persona jurídica no es necesario ingresar nombre y apellidos</aside>

## Obtener un Request específico

> Example

```shell
curl "https://api.legalbox.cl/s/requests/d4f0d7f0-79f2-49c0-845c-a92b67c8995a" \
  -H "Authorization: AUTH_TOKEN"
```

> Response

```json
{
    "request_id": "d4f0d7f0-79f2-49c0-845c-a92b67c8995a",
    "created_at": 1654029037,
    "params": {
      "tipo": "juridico",
      "rut": "93307000",
      "dv": "k"
    },
    "status": "done",
    "count": 4,
    "time": 630
}
```

### HTTP Request

`GET https://api.legalbox.cl/s/requests/<REQUEST_ID>`

### URL Parameters

Parameter | Type | Description
--------- | ------ | -----------
REQUEST_ID | (string) | ID de la Request


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
count | (integer)| Número de causas encontradas




## Obtener todos mis Requests

> Example

```shell
curl "https://api.legalbox.cl/s/requests" \
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
    "count": 4,
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
    "count": 0,
    "time": 945
  }
]

```

### HTTP Request

`GET https://api.legalbox.cl/s/requests`


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
count | (integer)| Número de causas encontradas




