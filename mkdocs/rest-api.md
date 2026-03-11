RevelDigital REST API
=====================
Provides REST based access to your Revel Digital account.

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

The `api_key` can be included in a query string parameter and should be included in each request.

```sh
$curl -i https://api.reveldigital.com/account?api_key=<your key here>
```

- **Header (More Secure)**

To use header based authentication, include the `X-RevelDigital-ApiKey: <your key here>` header value.

```sh
$curl -i -H "X-RevelDigital-ApiKey: <your key here>" https://api.reveldigital.com/account
```

- **OAuth 2.0 (Most secure)**

OAuth is a standard protocol for the exchange of an authorization token. This method requires a user login rather than an API key.

!!! Note
    Users must be assigned to the `API` role in order to access the API programatically.

Use the following for configuration of your OAuth client:

```
Client ID: RevelDigital
Required scope: webapi
Authorization URL: https://id.reveldigital.com/connect/authorize
Token URL: https://id.reveldigital.com/connect/token
Well known endpoint: https://id.reveldigital.com/.well-known/openid-configuration
```

##### Data Format

All data with the exception of media uploads is in `JSON` format. This includes POST body data. Request headers should include
the following to specify JSON as the content type.

```
Content-Type: application/json
```

Timestamps are returned in ISO 8601 format:

```sh
YYYY-MM-DDTHH:MM:SSZ
```

##### Pagination

Most list endpoints support pagination using the following query parameters:

| Parameter | Description |
|-----------|-------------|
| `take` | Maximum number of items to return |
| `page` | Page number (0-based) |

##### JSON Patch

Several endpoints support partial updates using [JSON Patch](http://jsonpatch.com) syntax via the `PATCH` HTTP method.

```json
[
  { "op": "replace", "path": "/propertyName", "value": "new value" }
]
```

##### Cross Origin Resource Sharing

The API supports Cross Origin Resource Sharing (CORS) for AJAX requests. You can read the [CORS W3C working draft](https://www.w3.org/TR/cors/),
or [this intro](https://code.google.com/archive/p/html5security/wikis/CrossOriginRequestSecurity.wiki) from the HTML5 Security Guide.

---

### Account

Manage your Revel Digital account.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/account` | Gets account details |
| PUT | `/account` | Updates an account |
| GET | `/account/organizations` | Gets organizations |
| GET | `/account/auditevents` | Gets audit events for the account |
| GET | `/account/auditevents/{eventId}` | Gets a single audit event by ID |

??? info "GET /account/auditevents query parameters"

    | Parameter | Type | Description |
    |-----------|------|-------------|
    | `userId` | string | Filter by user ID |
    | `eventType` | string | Filter by event type |
    | `httpMethod` | string | Filter by HTTP method (GET, POST, PUT, DELETE) |
    | `controllerName` | string | Filter by controller name |
    | `actionName` | string | Filter by action name |
    | `startDate` | string | Filter events after this date (ISO 8601) |
    | `endDate` | string | Filter events before this date (ISO 8601) |
    | `ipAddress` | string | Filter by IP address |
    | `responseCode` | string | Filter by HTTP response code |
    | `limit` | integer | Maximum number of items to return (default: 100) |
    | `page` | integer | Page number for pagination (0-based) |

---

### AdHawk (Analytics)

Analytics and reporting endpoints for play logs, audience data, device metrics, and more.

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/adhawk/dataset` | Returns AdHawk dataset based on post parameters (legacy) |
| GET | `/adhawk/playlogs` | Gets play logs for the account |
| GET | `/adhawk/pinglogs` | Gets ping/heartbeat logs for the account |
| GET | `/adhawk/eventlogs` | Gets event logs for the account |
| GET | `/adhawk/eventmetrics` | Gets aggregated event metrics |
| GET | `/adhawk/eventflow` | Gets event flow data for Sankey visualizations |
| GET | `/adhawk/impressions` | Gets audience impressions for the account |
| GET | `/adhawk/devicemetrics` | Gets aggregated device health metrics |
| GET | `/adhawk/audiencemetrics` | Gets aggregated audience metrics |
| GET | `/adhawk/mediaplaystats` | Gets media play statistics aggregated by file |
| GET | `/adhawk/deviceplaystats` | Gets device play statistics aggregated by device |
| GET | `/adhawk/playstatsbytime` | Gets time-series play statistics by interval |
| GET | `/adhawk/heatmap` | Gets geographic heatmap data aggregated by location |
| GET | `/adhawk/mediaimpressions` | Gets media impressions (OTS) data by media file |
| GET | `/adhawk/devicemediaimpressions` | Gets media impressions data aggregated by device |

!!! Note
    Most AdHawk endpoints require `startDate` and `endDate` query parameters in ISO 8601 format. Optional filters include `deviceId`, `fileId`, `eventName`, `interval`, and `limit`.

??? info "Common AdHawk query parameters"

    | Parameter | Type | Description |
    |-----------|------|-------------|
    | `startDate` | string | Start date for the query (required, ISO 8601) |
    | `endDate` | string | End date for the query (required, ISO 8601) |
    | `deviceId` | array | Optional list of device IDs to filter by |
    | `fileId` | array | Optional list of file/media IDs to filter by |
    | `eventName` | array | Optional list of event names to filter by |
    | `interval` | string | Time interval for aggregation: `minute`, `hour`, `day`, `week`, `month` |
    | `groupByDevice` | boolean | Group results by device (default: false) |
    | `limit` | integer | Maximum number of results (default: 1000, max: 10000) |

---

### Alerts

Manage account alerts for device health and status.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/alerts` | Gets all alerts for the account |
| GET | `/alerts/{id}` | Gets an alert by ID |
| PUT | `/alerts/{id}` | Updates an alert (snooze or resolve) |
| PATCH | `/alerts/{id}` | Partially updates an alert using JSON Patch |

??? info "GET /alerts query parameters"

    | Parameter | Type | Description |
    |-----------|------|-------------|
    | `id` | string | Unique identifier for the alert |
    | `device_id` | array | Filter by device IDs |
    | `active_only` | boolean | Filter to show only active alerts (not resolved and not snoozed) |
    | `resolved` | boolean | Filter by resolved state |
    | `org_id` | string | Filter by organization ID |
    | `take` | integer | Maximum number of items to retrieve |
    | `page` | integer | Page number for pagination |

---

### DataTables

Manage structured data tables with full CRUD operations, versioning, and import/export capabilities.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/datatables` | Lists data tables in the account |
| POST | `/datatables` | Creates a new data table |
| GET | `/datatables/{tableId}` | Gets a data table definition by ID |
| PUT | `/datatables/{tableId}` | Updates a data table definition |
| DELETE | `/datatables/{tableId}` | Deletes a data table and all its rows |

##### Rows

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/datatables/{tableId}/rows` | Lists rows in a data table |
| POST | `/datatables/{tableId}/rows` | Creates a new row |
| GET | `/datatables/{tableId}/rows/{rowId}` | Gets a single row by ID |
| PUT | `/datatables/{tableId}/rows/{rowId}` | Updates a row (partial update) |
| DELETE | `/datatables/{tableId}/rows/{rowId}` | Deletes a row |

##### Batch Operations

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/datatables/{tableId}/rows/batch` | Batch creates rows |
| POST | `/datatables/{tableId}/rows/batch-delete` | Deletes multiple rows (max 100 per call) |
| PUT | `/datatables/{tableId}/rows/reorder` | Reorders rows |
| POST | `/datatables/{tableId}/rows/import` | Imports rows from CSV or Excel (.xlsx) |
| GET | `/datatables/{tableId}/rows/export` | Exports rows as CSV |

##### Row Versioning

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/datatables/{tableId}/rows/{rowId}/versions` | Lists version history for a row |
| GET | `/datatables/{tableId}/rows/{rowId}/versions/{version}` | Gets a specific version snapshot |
| POST | `/datatables/{tableId}/rows/{rowId}/rollback` | Rolls back a row to a specific version |

??? info "GET /datatables/{tableId}/rows query parameters"

    | Parameter | Type | Description |
    |-----------|------|-------------|
    | `filter` | string | Filter expression |
    | `sort` | string | Sort field |
    | `sortDir` | string | Sort direction |
    | `pageSize` | integer | Number of rows per page |
    | `continuationToken` | string | Token for fetching the next page |
    | `fields` | string | Specific fields to return |

---

### Devices

Manage devices, device groups, commands, and snapshots.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/devices` | Gets all devices in an account |
| POST | `/devices` | Registers a new device |
| GET | `/devices/{id}` | Gets a device by ID |
| PUT | `/devices/{id}` | Updates a device |
| DELETE | `/devices/{id}` | Deletes a device |
| PATCH | `/devices/{id}` | Patch a device (partial update via JSON Patch) |

##### Device Groups

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/devices/groups` | Gets device groups in the account |
| POST | `/devices/groups` | Creates a new device group |
| PUT | `/devices/groups/{id}` | Updates a device group |
| DELETE | `/devices/groups/{id}` | Deletes a device group |

##### Commands & Monitoring

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/devices/commands` | Sends commands to multiple devices |
| POST | `/devices/{id}/commands` | Sends commands to a specific device |
| POST | `/devices/{id}/track` | Creates an event associated with a device |
| GET | `/devices/pingdata` | Gets device ping data by registration key |
| GET | `/devices/{registrationKey}/pingdata` | Gets device ping data by registration key |
| GET | `/devices/{registrationKey}/snap` | Gets current snapshot of device screen (JPEG) |

??? info "GET /devices query parameters"

    | Parameter | Type | Description |
    |-----------|------|-------------|
    | `id` | string | Unique identifier for the device |
    | `take` | integer | Maximum number of items to retrieve |
    | `page` | integer | Page number for pagination |
    | `device_type_id` | string | Filter by device type |
    | `group_id` | array | Filter by group IDs |
    | `group_name` | array | Filter by group names |
    | `include_snap` | boolean | Include snapshot of currently playing content (base64 JPEG) |
    | `org_id` | string | Filter by organization ID |
    | `is_online` | boolean | Filter by online status |

---

### Media

Upload, manage, and organize media assets.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/media` | Gets all media in an account |
| POST | `/media` | Uploads a new media asset |
| GET | `/media/{id}` | Gets a media item by ID |
| PUT | `/media/{id}` | Updates media asset properties |
| DELETE | `/media/{id}` | Deletes a media asset |
| PATCH | `/media/{id}` | Patch a media item (partial update via JSON Patch) |
| POST | `/media/{group_id}/{file_name}` | Uploads a new media asset to a specific group |
| POST | `/media/import` | Imports a file from a URL |

##### Media Groups

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/media/groups` | Gets media groups |
| POST | `/media/groups` | Creates a new media group |
| PUT | `/media/groups/{id}` | Updates a media group |
| DELETE | `/media/groups/{id}` | Deletes a media group |

??? info "GET /media query parameters"

    | Parameter | Type | Description |
    |-----------|------|-------------|
    | `id` | string | Media ID to filter by |
    | `take` | integer | Maximum number of items to return |
    | `page` | integer | Page number for pagination |
    | `group_id` | array | Filter by media group IDs |
    | `group_name` | array | Filter by group names |

---

### Playlists

Manage playlists and playlist groups.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/playlists` | Gets all playlists in an account |
| POST | `/playlists` | Creates a new playlist |
| GET | `/playlists/{id}` | Gets a playlist by ID |
| PUT | `/playlists/{id}` | Replaces a playlist |
| DELETE | `/playlists/{id}` | Deletes a playlist |
| PATCH | `/playlists/{id}` | Patch a playlist (partial update via JSON Patch) |

##### Playlist Groups

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/playlists/groups` | Gets playlist groups in the account |
| POST | `/playlists/groups` | Creates a new playlist group |
| PUT | `/playlists/groups/{id}` | Updates a playlist group |
| DELETE | `/playlists/groups/{id}` | Deletes a playlist group |

---

### Schedules

Manage schedules and schedule groups.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/schedules` | Gets schedules in an account |
| POST | `/schedules` | Creates a new schedule |
| GET | `/schedules/{id}` | Gets a schedule by ID |
| PUT | `/schedules/{id}` | Updates a schedule |
| DELETE | `/schedules/{id}` | Deletes a schedule |
| PATCH | `/schedules/{id}` | Patch a schedule (partial update via JSON Patch) |

##### Schedule Groups

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/schedules/groups` | Gets schedule groups in the account |
| POST | `/schedules/groups` | Creates a new schedule group |
| PUT | `/schedules/groups/{id}` | Updates a schedule group |
| DELETE | `/schedules/groups/{id}` | Deletes a schedule group |

??? info "GET /schedules query parameters"

    | Parameter | Type | Description |
    |-----------|------|-------------|
    | `id` | string | Schedule ID to filter by |
    | `take` | integer | Maximum number of items to return |
    | `page` | integer | Page number for pagination |
    | `group_id` | array | Filter by schedule group IDs |
    | `group_name` | array | Filter by group names |
    | `device_id` | string | Filter by device ID |

---

### Templates

Manage templates and template groups.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/templates` | Gets all templates in an account |
| GET | `/templates/{id}` | Gets a template by ID |
| DELETE | `/templates/{id}` | Deletes a template |

##### Template Groups

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/templates/groups` | Gets template groups in the account |
| POST | `/templates/groups` | Creates a new template group |
| PUT | `/templates/groups/{id}` | Updates a template group |
| DELETE | `/templates/groups/{id}` | Deletes a template group |

---

### Users

Access user information for the account.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/users` | Gets all users in an account |
| GET | `/users/{id}` | Gets a user by ID |

---

### Report

Generate and export reports.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/report` | Returns a list of reports available for export |
| POST | `/report/export` | Generate and export a report |

---

### Swagger

[Interactive API documentation provided by Swagger](https://api.reveldigital.com/swagger/)

!!! Note
    The Revel Digital API is also available on Postman here: [https://www.postman.com/reveldigital](https://www.postman.com/reveldigital)
