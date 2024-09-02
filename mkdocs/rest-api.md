RevelDigital REST API
=====================
Provides REST based access to your RevelDigital account.

!!! Note
     See our [Swagger](https://api.reveldigital.com/swagger/) or [Postman](https://www.postman.com/reveldigital) websites for interactive documentation.
     
### Getting Started

##### API Endpoint

All API access originates from `https://api.reveldigital.com`

##### Authentication

!!! Note
    A valid API key is required for each request.
    API keys are available in your Revel Digital account under [Account > Developer API](https://as1.reveldigital.com/account/api).

There are three methods of authentication available including:

- **Query Parameter**

The `api_key` can be included in a query string parameter and shoud be included in each request.

```sh
$curl -i https://api.reveldigital.com/account?api_key=<your key here>
```

- **Header (More Secure)**

To use header based authentication, include the `X-RevelDigital-API: <your key here>` header value.

- **OAuth 2.0 (Most secure)**

OAuth is a standard protocol for the exchange of an authorization token. This method requires a user login rather than an API key.

!!! Note
    Users must be assigned to the `API` role in order to access the API programatically.

Use the following for configuration of your OAuth client:

```
Client ID: RevelDigital
Requried scope: webapi
Well known endpoint: https://id.reveldigital.com/.well-known/openid-configuration
```
#####Data Format#####

All data with the exception of media uploads is in `JSON` format. This includes POST body data. Request headers should include
the following to specify JSON as the content type.

```
Content-Type: application/json
```

Timestamps are returned in ISO 8601 format:

```sh
YYYY-MM-DDTHH:MM:SSZ
```

##### Cross Origin Resource Sharing

The API supports Cross Origin Resource Sharing (CORS) for AJAX requests. You can read the [CORS W3C working draft](https://www.w3.org/TR/cors/),
or [this intro](https://code.google.com/archive/p/html5security/wikis/CrossOriginRequestSecurity.wiki) from the HTML5 Security Guide.


### Swagger

[Interactive API documentation provided by Swagger](https://api.reveldigital.com/swagger/)

!!! Note
    The Revel Digital API is also available on Postman here: [https://www.postman.com/reveldigital](https://www.postman.com/reveldigital)

