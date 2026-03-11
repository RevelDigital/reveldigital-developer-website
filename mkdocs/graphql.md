Revel Digital GraphQL API
=========================

The Revel Digital GraphQL API provides a flexible, strongly-typed interface for querying and mutating your account data. Unlike the REST API, GraphQL allows you to request exactly the fields you need in a single request, reducing payload size and eliminating over-fetching.

!!! Note
    The full SDL (Schema Definition Language) is available at [https://api.reveldigital.com/graphql/?sdl](https://api.reveldigital.com/graphql/?sdl)

### Getting Started

##### Endpoint

All GraphQL requests are sent to:

```
https://api.reveldigital.com/graphql
```

##### Authentication

The GraphQL API uses the same authentication methods as the REST API:

- **Header (Recommended)** — Include `X-RevelDigital-ApiKey: <your key here>`
- **Query Parameter** — Append `?api_key=<your key here>` to the endpoint URL
- **OAuth 2.0** — Use a Bearer token from the Revel Digital identity provider

!!! Note
    API keys are available in your Revel Digital account under [Account > Developer API](https://as1.reveldigital.com/account/api).
    Users must be assigned to the `API` role for programmatic access.

##### Making Requests

Send a `POST` request with a JSON body containing a `query` field (and optionally `variables`):

```sh
curl -X POST https://api.reveldigital.com/graphql \
  -H "Content-Type: application/json" \
  -H "X-RevelDigital-ApiKey: <your key here>" \
  -d '{
    "query": "{ device { id name isOnline } }"
  }'
```

##### Checking Permissions

The `permissions` query returns the current user's access rights. AI agents and integrations should call this at the start of each session to determine which operations are available.

```graphql
{
  permissions {
    isAdministrator
    permissions {
      resource
      canView
      canEdit
      canDelete
    }
    allowedMutations
    deniedMutations
  }
}
```

---

### Queries

All queries require authentication. Each query is protected by an authorization policy listed below.

#### Content Management

##### device
Gets devices in the account. Requires `Devices_View`.

```graphql
{
  device(
    id: ["device-id"]
    groupId: ["group-id"]
    groupName: ["Lobby"]
    tag: ["kiosk"]
    limit: 10
  ) {
    id
    name
    isOnline
    tags
    deviceType { name manufacturer }
    pingData {
      cpuUsage
      memoryUsage
      diskUsage
      playerVersion
      ipAddress
      timestamp
    }
    location { city state country latitude longitude }
  }
}
```

??? info "device arguments"

    | Argument | Type | Description |
    |----------|------|-------------|
    | `id` | [String!] | Filter by device IDs |
    | `groupId` | [String!] | Filter by group IDs |
    | `groupName` | [String!] | Filter by group names |
    | `deviceTypeId` | [String!] | Filter by device type IDs |
    | `includeSnap` | Boolean | Include device screenshot |
    | `orgId` | String | Filter by organization ID |
    | `tag` | [String!] | Filter by tags |
    | `limit` | Int | Maximum results |
    | `where` | DeviceFilterInput | Advanced filtering |
    | `order` | [DeviceSortInput!] | Sorting |

##### deviceGroups
Gets device groups. Requires `Devices_View`.

```graphql
{
  deviceGroups(tree: true) {
    id
    name
    count
    level
    children { id name count }
  }
}
```

##### media
Gets media assets. Requires `Files_View`.

```graphql
{
  media(groupName: ["Images"], limit: 20) {
    id
    name
    fileName
    mimeType
    fileSize
    fileUrl
    thumbnailUrl
    uploadedOn
    width
    height
    tags
  }
}
```

??? info "media arguments"

    | Argument | Type | Description |
    |----------|------|-------------|
    | `id` | [String!] | Filter by media IDs |
    | `groupId` | [String!] | Filter by group IDs |
    | `groupName` | [String!] | Filter by group names |
    | `orgId` | String | Filter by organization ID |
    | `tag` | [String!] | Filter by tags |
    | `limit` | Int | Maximum results |
    | `where` | MediaFilterInput | Advanced filtering |
    | `order` | [MediaSortInput!] | Sorting |

##### mediaGroups
Gets media groups. Requires `Files_View`.

##### playlist
Gets playlists. Requires `Playlists_View`.

```graphql
{
  playlist(limit: 10) {
    id
    name
    type
    duration
    calculatedDuration
    sources {
      id
      name
      type
      sequence
      interval
      media { fileName fileUrl }
    }
  }
}
```

##### playlistGroups
Gets playlist groups. Requires `Playlists_View`.

##### template
Gets templates. Requires `Templates_View`.

```graphql
{
  template(limit: 10) {
    id
    name
    width
    height
    orientation
    modules {
      id
      name
      type
      left
      top
      width
      height
      playlistId
    }
  }
}
```

##### templateGroups
Gets template groups. Requires `Templates_View`.

##### schedule
Gets schedules. Requires `Schedules_View`.

```graphql
{
  schedule(deviceId: "device-id") {
    id
    name
    startDate
    endDate
    startTime
    endTime
    monday
    tuesday
    wednesday
    thursday
    friday
    saturday
    sunday
    priority
    templateId
    playlistId
    devices { id }
  }
}
```

??? info "schedule arguments"

    | Argument | Type | Description |
    |----------|------|-------------|
    | `id` | [String!] | Filter by schedule IDs |
    | `groupId` | [String!] | Filter by group IDs |
    | `groupName` | [String!] | Filter by group names |
    | `deviceId` | String | Filter by device ID |
    | `orgId` | String | Filter by organization ID |
    | `tag` | [String!] | Filter by tags |
    | `limit` | Int | Maximum results |

##### scheduleGroups
Gets schedule groups. Requires `Schedules_View`.

##### user
Gets users. Requires `Account_ManageUsers_View`.

```graphql
{
  user {
    id
    firstName
    lastName
    email
    username
    role
    lastActivity
  }
}
```

##### alert
Gets alerts. Requires `Alerts_View`.

```graphql
{
  alert(activeOnly: true) {
    id
    createdOn
    isActive
    alertRule { id name ruleSet isEnabled }
    devices { id name }
    snoozedUntil
    resolvedOn
  }
}
```

##### auditEvent
Gets audit events. Requires `AuditEventsOwnerOnly` (account owners only).

```graphql
{
  auditEvent(
    startDate: "2025-01-01T00:00:00Z"
    endDate: "2025-01-31T23:59:59Z"
    limit: 50
  ) {
    eventId
    timestamp
    eventType
    userName
    httpMethod
    controllerName
    actionName
    ipAddress
    responseCode
  }
}
```

##### displayCommands
Gets the device commands configured for the account. Requires `Devices_View`.

```graphql
{
  displayCommands {
    name
    command
    arg
  }
}
```

#### Data Tables

##### dataTables
Lists data tables with pagination. Requires `DataTables_View`.

```graphql
{
  dataTables(pageSize: 20) {
    data { id name description columnCount rowCount updatedAt }
    continuationToken
  }
}
```

##### dataTable
Gets a single data table definition including column schema. Requires `DataTables_View`.

```graphql
{
  dataTable(tableId: "table-id") {
    id
    name
    description
    rowCount
    cacheTtlSeconds
    columns {
      id
      name
      key
      type
      required
      sortable
      options
      default
    }
  }
}
```

##### dataTableRows
Lists rows with optional filtering, sorting, and field selection. Requires `DataTables_View`.

```graphql
{
  dataTableRows(
    tableId: "table-id"
    filter: "{\"status\":\"active\"}"
    sort: "name"
    sortDir: "asc"
    pageSize: 50
  ) {
    data { id sortOrder data updatedAt }
    totalCount
    continuationToken
  }
}
```

##### dataTableRow
Gets a single row by ID. Requires `DataTables_View`.

##### exportDataTableRows
Exports all rows as a CSV string. Requires `DataTables_View`.

##### dataTableRowVersions
Lists version history for a row (newest first). Requires `DataTables_View`.

##### dataTableRowVersion
Gets a specific version snapshot of a row. Requires `DataTables_View`.

#### Analytics (AdHawk)

All analytics queries require `AdHawk_View` and accept `startDate` and `endDate` (ISO 8601, required).

##### playLogs
Content playback history.

```graphql
{
  playLogs(
    startDate: "2025-01-01T00:00:00Z"
    endDate: "2025-01-31T23:59:59Z"
    deviceId: ["device-id"]
    limit: 100
  ) {
    id
    timestamp
    deviceId
    fileId
    fileName
    duration
    type
  }
}
```

##### pingLogs
Device heartbeat/health data including CPU, memory, and disk usage.

```graphql
{
  pingLogs(
    startDate: "2025-01-01T00:00:00Z"
    endDate: "2025-01-31T23:59:59Z"
    limit: 100
  ) {
    id
    timestamp
    deviceId
    cpuUsage
    memoryUsage
    diskUsage
    ipAddress
    externalIpAddress
  }
}
```

##### eventLogs
Custom events generated by devices or applications.

##### eventMetrics
Aggregated event metrics with support for interval-based aggregation.

```graphql
{
  eventMetrics(
    startDate: "2025-01-01T00:00:00Z"
    endDate: "2025-01-31T23:59:59Z"
    interval: DAY
    groupByEvent: true
  ) {
    eventName
    periodStart
    periodEnd
    totalEvents
    uniqueSessions
  }
}
```

##### impressions
Audience detection data from sensors (motion, face detection, BLE, WiFi).

##### deviceMetrics
Aggregated device health metrics for fleet monitoring.

```graphql
{
  deviceMetrics(
    startDate: "2025-01-01T00:00:00Z"
    endDate: "2025-01-31T23:59:59Z"
    interval: DAY
  ) {
    deviceId
    deviceName
    periodStart
    periodEnd
    avgCpuUsage
    maxCpuUsage
    avgMemoryUsage
    maxMemoryUsage
    uptimePercentage
    alertCount
  }
}
```

##### audienceMetrics
Aggregated audience demographics, traffic, and engagement data.

```graphql
{
  audienceMetrics(
    startDate: "2025-01-01T00:00:00Z"
    endDate: "2025-01-31T23:59:59Z"
    interval: DAY
    includeDwellTime: true
  ) {
    deviceId
    deviceName
    periodStart
    totalImpressions
    uniqueVisitors
    avgDwellTime
    maleCount
    femaleCount
    ageUnder18
    age18To24
    age25To34
    age35To44
    age45To54
    age55To64
    age65To74
    ageOver74
  }
}
```

##### mediaPlayStats
Media performance aggregated by file.

##### devicePlayStats
Device playback summary aggregated by device.

##### deviceMediaPlayStats
Combined device/media analysis — what content played on which devices.

##### playStatsByTime
Time-series playback trends with configurable intervals.

```graphql
{
  playStatsByTime(
    startDate: "2025-01-01T00:00:00Z"
    endDate: "2025-01-31T23:59:59Z"
    interval: DAY
    groupByFile: true
  ) {
    fileId
    fileName
    periodStart
    periodEnd
    totalPlays
    totalDuration
    avgDuration
  }
}
```

##### eventFlow
User navigation paths for Sankey-type visualizations.

##### heatMapData
Geographic impression data aggregated by location.

##### eventHeatMapData
Geographic event data aggregated by location.

##### mediaImpressions
OTS (Opportunity To See) metrics aggregated by media file.

##### deviceMediaImpressions
OTS metrics aggregated by device.

---

### Mutations

All mutations require authentication and are protected by authorization policies.

#### Data Table Management

##### createDataTable
Creates a new data table with a column schema. Requires `DataTables_Edit`.

```graphql
mutation {
  createDataTable(input: {
    name: "Menu Board"
    description: "Restaurant menu items"
    columns: [
      { name: "Item", key: "item", type: TEXT, required: true },
      { name: "Price", key: "price", type: TEXT },
      { name: "Description", key: "desc", type: TEXT }
    ]
  }) {
    success
    table { id name columns { id key name type } }
    error
  }
}
```

##### updateDataTable
Updates a data table definition. Requires `DataTables_Edit`.

##### deleteDataTable
Deletes a data table and all its rows. Requires `DataTables_Delete`.

```graphql
mutation {
  deleteDataTable(tableId: "table-id") {
    success
    error
  }
}
```

##### createDataTableRow
Creates a new row. Requires `DataTables_Edit`.

```graphql
mutation {
  createDataTableRow(input: {
    tableId: "table-id"
    data: { item: "Burger", price: "$9.99", desc: "Classic cheeseburger" }
  }) {
    success
    row { id data updatedAt }
    error
  }
}
```

##### updateDataTableRow
Updates a row (partial update). Requires `DataTables_Edit`.

##### deleteDataTableRow
Deletes a row. Requires `DataTables_Delete`.

##### batchCreateDataTableRows
Batch creates up to 100 rows. Requires `DataTables_Edit`.

```graphql
mutation {
  batchCreateDataTableRows(input: {
    tableId: "table-id"
    rows: [
      { data: { item: "Burger", price: "$9.99" } },
      { data: { item: "Fries", price: "$4.99" } }
    ]
  }) {
    success
    results { rowId success error }
    error
  }
}
```

##### batchDeleteDataTableRows
Batch deletes up to 100 rows. Requires `DataTables_Delete`.

##### importDataTableRows
Imports rows from CSV content. Requires `DataTables_Edit`.

##### reorderDataTableRows
Reorders rows by specifying the desired row ID sequence. Requires `DataTables_Edit`.

##### rollbackDataTableRow
Rolls back a row to a previous version. Requires `DataTables_Edit`.

```graphql
mutation {
  rollbackDataTableRow(input: {
    tableId: "table-id"
    rowId: "row-id"
    version: 2
  }) {
    success
    newVersion
    restoredRow { id data updatedAt }
    error
  }
}
```

#### Device Commands

##### sendDeviceCommand
Sends commands to a specific device. Requires `Devices_Edit`.

Known commands: `restart`, `reboot`, `screenshot`, `refresh`, `display_on`, `display_off`, `volume` (arg: 0-100), `clear_cache`, `update`.

```graphql
mutation {
  sendDeviceCommand(
    deviceId: "device-id"
    commands: [{ command: "volume", arg: "50" }]
  ) {
    success
    deviceId
    commandCount
    error
  }
}
```

##### sendBulkDeviceCommands
Sends commands to multiple devices at once. Requires `Devices_Edit`.

```graphql
mutation {
  sendBulkDeviceCommands(input: {
    deviceIds: ["device-1", "device-2"]
    commands: [{ command: "restart" }]
  }) {
    totalDevices
    successCount
    failureCount
    results { success deviceId error }
  }
}
```

#### Media Management

##### createMediaFromUrl
Creates a new media asset by downloading from a URL. Requires `Files_Edit`.

```graphql
mutation {
  createMediaFromUrl(input: {
    url: "https://example.com/image.jpg"
    name: "Promo Image"
    groupId: "group-id"
  }) {
    success
    media { id name fileUrl }
    error
  }
}
```

##### updateMedia
Updates media metadata (does not replace the file). Requires `Files_Edit`.

##### deleteMedia
Deletes a media asset. Requires `Files_Delete`.

#### Playlist Management

##### addPlaylistSource
Adds a content source to a playlist. Requires `Playlists_Edit`.

```graphql
mutation {
  addPlaylistSource(input: {
    playlistId: "playlist-id"
    fileId: "media-file-id"
    interval: 10
  }) {
    success
    playlist {
      id
      name
      sources { id name sequence }
    }
    error
  }
}
```

##### updatePlaylistSource
Updates a source within a playlist. Requires `Playlists_Edit`.

##### removePlaylistSource
Removes a source from a playlist. Requires `Playlists_Edit`.

```graphql
mutation {
  removePlaylistSource(
    playlistId: "playlist-id"
    sourceId: "source-id"
  ) {
    success
    error
  }
}
```

##### reorderPlaylistSources
Reorders sources within a playlist. Requires `Playlists_Edit`.

---

### Filtering & Sorting

All list queries support advanced filtering via `where` and sorting via `order` arguments using Hot Chocolate-style filter inputs.

##### Filtering

Use field-specific operators to build filter expressions:

```graphql
{
  device(where: {
    name: { contains: "Lobby" }
    isOnline: { eq: true }
  }) {
    id
    name
    isOnline
  }
}
```

Common filter operators:

| Operator | Description |
|----------|-------------|
| `eq` | Equal to |
| `neq` | Not equal to |
| `contains` | Contains substring |
| `startsWith` | Starts with |
| `endsWith` | Ends with |
| `gt` / `gte` | Greater than / greater or equal |
| `lt` / `lte` | Less than / less or equal |
| `in` / `nin` | In / not in list |

##### Sorting

Use the `order` argument to sort results:

```graphql
{
  media(order: [{ uploadedOn: DESC }]) {
    id
    name
    uploadedOn
  }
}
```

---

### Enums

| Enum | Values | Description |
|------|--------|-------------|
| `AdHawkIntervalType` | `MINUTE`, `HOUR`, `DAY`, `WEEK`, `MONTH` | Time aggregation interval |
| `AdHawkGender` | `MALE`, `FEMALE`, `UNKNOWN` | Detected visitor gender |
| `AdHawkAgeRange` | `UNDER18`, `AGE18TO24`, `AGE25TO34`, `AGE35TO44`, `AGE45TO54`, `AGE55TO64`, `AGE65TO74`, `AGEOVER74` | Age group classification |
| `ColumnType` | Various | Data table column type |
| `SortEnumType` | `ASC`, `DESC` | Sort direction |
| `PlaylistType` | Various | Content collection type |
| `SourceType` | Various | Content source category |
| `ScheduleType` | Various | Schedule classification |

---

### Authorization Policies

Access to queries and mutations is controlled by role-based policies:

| Policy | Description |
|--------|-------------|
| `Devices_View` / `Devices_Edit` / `Devices_Delete` | Device management |
| `Files_View` / `Files_Edit` / `Files_Delete` | Media asset management |
| `Playlists_View` / `Playlists_Edit` / `Playlists_Delete` | Playlist operations |
| `Templates_View` / `Templates_Edit` / `Templates_Delete` | Template operations |
| `Schedules_View` / `Schedules_Edit` / `Schedules_Delete` | Schedule operations |
| `Alerts_View` | Alert access |
| `DataTables_View` / `DataTables_Edit` / `DataTables_Delete` | Data table operations |
| `AdHawk_View` | Analytics data access |
| `Account_ManageUsers_View` | User management |
| `AuditEventsOwnerOnly` | Audit log access (account owners only) |

!!! Tip
    Use the `permissions` query to programmatically check which operations are available for your API key or user account.
