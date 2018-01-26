RevelDigital API
================
The RevelDigital API provides REST based access to your RevelDigital account

**Version:** v1


### /api/account
---
##### ***GET***
**Summary:** Gets account details.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns account details | [RevelDigital.Core.PublicApi.Models.Account](#reveldigital.core.publicapi.models.account) |

##### ***PUT***
**Summary:** Updates an account.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| account | body |  | No | [RevelDigital.Core.PublicApi.Models.Account](#reveldigital.core.publicapi.models.account) |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | If account was updated successfully |
| 400 | If the account API key is invalid |

### /api/devices
---
##### ***GET***
**Summary:** Gets all devices in an account.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | query |  | No | string |
| take | query |  | No | integer |
| page | query |  | No | integer |
| device_type_id | query |  | No | string |
| group_id | query |  | No | [ string ] |
| group_name | query |  | No | [ string ] |
| include_snap | query |  | Yes | boolean |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns an array of devices | [ [RevelDigital.Core.PublicApi.Models.Device](#reveldigital.core.publicapi.models.device) ] |

##### ***POST***
**Summary:** Creates a device.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| activation_code | query |  | No | string |
| device | body |  | No | [RevelDigital.Core.PublicApi.Models.DeviceRequest](#reveldigital.core.publicapi.models.devicerequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Returns the newly created device | [RevelDigital.Core.PublicApi.Models.Device](#reveldigital.core.publicapi.models.device) |
| 400 | If the registration code is invalid |

### /api/devices/{id}
---
##### ***GET***
**Summary:** Gets a device by ID.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns the device matching the ID | [RevelDigital.Core.PublicApi.Models.Device](#reveldigital.core.publicapi.models.device) |

##### ***PUT***
**Summary:** Updates a device.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |
| device | body |  | No | [RevelDigital.Core.PublicApi.Models.DeviceRequest](#reveldigital.core.publicapi.models.devicerequest) |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | If device was updated successfully |
| 400 | If the device ID is invalid |

##### ***DELETE***
**Summary:** Delete a device.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

### /api/devices/groups
---
##### ***GET***
**Summary:** Gets device groups in the account.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | query |  | No | string |
| take | query |  | No | integer |
| page | query |  | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns an array of device groups | [ [RevelDigital.Core.PublicApi.Models.Group](#reveldigital.core.publicapi.models.group) ] |

##### ***POST***
**Summary:** Create a new device group.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| group | body | Device group | No | [RevelDigital.Core.PublicApi.Models.GroupRequest](#reveldigital.core.publicapi.models.grouprequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Returns the newly-created item | [RevelDigital.Core.PublicApi.Models.Group](#reveldigital.core.publicapi.models.group) |
| 400 | If the item is null |

### /api/devices/groups/{id}
---
##### ***PUT***
**Summary:** Updates a device group.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query | API key | No | string |
| id | path | Group id | Yes | string |
| group | body | Device group | No | [RevelDigital.Core.PublicApi.Models.GroupRequest](#reveldigital.core.publicapi.models.grouprequest) |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

##### ***DELETE***
**Summary:** Delete a device group.

**Description:** Group must be empty.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

### /api/devices/pingdata
---
##### ***GET***
**Summary:** Gets device ping data by registration key.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| key | query |  | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns ping data for the device | [RevelDigital.Core.PublicApi.Models.PingData](#reveldigital.core.publicapi.models.pingdata) |

### /api/devices/{registrationkey}/snap
---
##### ***GET***
**Summary:** Gets current snapshot of the device screen.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| registrationKey | path |  | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Returns snapshot |

### /api/devices/{registrationkey}/pingdata
---
##### ***GET***
**Summary:** Gets device ping data by registration key.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| registrationKey | path |  | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns ping data for the device | [RevelDigital.Core.PublicApi.Models.PingData](#reveldigital.core.publicapi.models.pingdata) |

### /api/devices/commands
---
##### ***POST***
**Summary:** Sends a collection of commands to devices.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| commandSet | body |  | No | [ [RevelDigital.Core.PublicApi.Models.DeviceCommand](#reveldigital.core.publicapi.models.devicecommand) ] |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Commands delivered successfully |

### /api/devices/{id}/commands
---
##### ***POST***
**Summary:** Sends a collection of commands to a specific device.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |
| commands | body |  | No | [ [RevelDigital.Core.PublicApi.Models.Command](#reveldigital.core.publicapi.models.command) ] |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Commands delivered successfully |

### /api/media
---
##### ***GET***
**Summary:** Gets all media in an account.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | query |  | No | string |
| take | query |  | No | integer |
| page | query |  | No | integer |
| group_id | query |  | No | [ string ] |
| group_name | query |  | No | [ string ] |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns an array of media | [ [RevelDigital.Core.PublicApi.Models.Media](#reveldigital.core.publicapi.models.media) ] |

##### ***POST***
**Summary:** Uploads new media

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| group_id | query |  | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Returns the newly created media | [RevelDigital.Core.PublicApi.Models.Media](#reveldigital.core.publicapi.models.media) |
| 400 | If the API key is invalid or upload was not supplied |

### /api/media/{id}
---
##### ***GET***
**Summary:** Gets media by ID.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns the media matching the ID | [RevelDigital.Core.PublicApi.Models.Media](#reveldigital.core.publicapi.models.media) |

##### ***PUT***
**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |
| media | body |  | No | [RevelDigital.Core.PublicApi.Models.MediaRequest](#reveldigital.core.publicapi.models.mediarequest) |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

##### ***DELETE***
**Summary:** Delete a device.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

### /api/media/groups
---
##### ***GET***
**Summary:** Gets media groups in the account.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | query |  | No | string |
| take | query |  | No | integer |
| page | query |  | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns an array of device groups | [ [RevelDigital.Core.PublicApi.Models.Group](#reveldigital.core.publicapi.models.group) ] |

##### ***POST***
**Summary:** Create a new media group.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| group | body | Media group | No | [RevelDigital.Core.PublicApi.Models.GroupRequest](#reveldigital.core.publicapi.models.grouprequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Returns the newly-created item | [RevelDigital.Core.PublicApi.Models.Group](#reveldigital.core.publicapi.models.group) |
| 400 | If the item is null |

### /api/media/groups/{id}
---
##### ***PUT***
**Summary:** Updates a media group.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query | API key | No | string |
| id | path | Group id | Yes | string |
| group | body | Device group | No | [RevelDigital.Core.PublicApi.Models.GroupRequest](#reveldigital.core.publicapi.models.grouprequest) |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

##### ***DELETE***
**Summary:** Delete a media group.

**Description:** Group must be empty.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

### /api/media/{group_id}/{file_name}
---
##### ***POST***
**Summary:** Uploads new media

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| group_id | path |  | Yes | string |
| file_name | path |  | Yes | string |
| api_key | query |  | No | string |
| shared | query |  | Yes | boolean |
| start_date | query |  | No | dateTime |
| end_date | query |  | No | dateTime |
| advertiser_id | query |  | No | integer |
| name | query |  | No | string |
| description | query |  | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Returns the newly created media | [RevelDigital.Core.PublicApi.Models.Media](#reveldigital.core.publicapi.models.media) |
| 400 | If the API key is invalid |

### /api/media/import
---
##### ***POST***
**Summary:** Import a file from a URL.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query | API key | No | string |
| url | query | URL of the file to import | No | string |
| group_id | query |  | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Returns the newly created media | [RevelDigital.Core.PublicApi.Models.Media](#reveldigital.core.publicapi.models.media) |
| 400 | If the API key is invalid or upload was not supplied |

### /api/playlists
---
##### ***GET***
**Summary:** Gets all playlists in an account.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | query |  | No | string |
| take | query |  | No | integer |
| page | query |  | No | integer |
| group_id | query |  | No | [ string ] |
| group_name | query |  | No | [ string ] |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns an array of playlists | [ [RevelDigital.Core.PublicApi.Models.Playlist](#reveldigital.core.publicapi.models.playlist) ] |

### /api/playlists/{id}
---
##### ***GET***
**Summary:** Gets a playlist by ID.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns the playlist matching the ID | [RevelDigital.Core.PublicApi.Models.Playlist](#reveldigital.core.publicapi.models.playlist) |

##### ***PUT***
**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |
| playlist | body |  | No | [RevelDigital.Core.PublicApi.Models.Playlist](#reveldigital.core.publicapi.models.playlist) |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

##### ***DELETE***
**Summary:** Delete a playlist.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

### /api/playlists/groups
---
##### ***GET***
**Summary:** Gets playlist groups in the account.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | query |  | No | string |
| take | query |  | No | integer |
| page | query |  | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns an array of playlist groups | [ [RevelDigital.Core.PublicApi.Models.Group](#reveldigital.core.publicapi.models.group) ] |

##### ***POST***
**Summary:** Create a new playlist group.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| group | body | Playlist group | No | [RevelDigital.Core.PublicApi.Models.GroupRequest](#reveldigital.core.publicapi.models.grouprequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Returns the newly-created item | [RevelDigital.Core.PublicApi.Models.Group](#reveldigital.core.publicapi.models.group) |
| 400 | If the item is null |

### /api/playlists/groups/{id}
---
##### ***PUT***
**Summary:** Updates a playlist group.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query | API key | No | string |
| id | path | Group id | Yes | string |
| group | body | Device group | No | [RevelDigital.Core.PublicApi.Models.GroupRequest](#reveldigital.core.publicapi.models.grouprequest) |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

##### ***DELETE***
**Summary:** Delete a playlist group.

**Description:** Group must be empty.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

### /api/report/adhawk/impressions-by-gender
---
##### ***GET***
**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| start | query |  | Yes | dateTime |
| end | query |  | Yes | dateTime |
| gender | query |  | No | [ string ] |
| device_id | query |  | No | [ string ] |
| compare_start | query |  | No | dateTime |
| compare_end | query |  | No | dateTime |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |

### /api/report/adhawk/impressions-by-hour
---
##### ***GET***
**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| start | query |  | Yes | dateTime |
| end | query |  | Yes | dateTime |
| interval | query |  | Yes | integer |
| metric | query |  | Yes | integer |
| device_id | query |  | No | [ string ] |
| compare_start | query |  | No | dateTime |
| compare_end | query |  | No | dateTime |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |

### /api/report/adhawk/impressions-by-age
---
##### ***GET***
**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| start | query |  | Yes | dateTime |
| end | query |  | Yes | dateTime |
| interval | query |  | Yes | integer |
| metric | query |  | Yes | integer |
| device_id | query |  | No | [ string ] |
| compare_start | query |  | No | dateTime |
| compare_end | query |  | No | dateTime |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |

### /api/report/adhawk/device-detail
---
##### ***GET***
**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| start | query |  | Yes | dateTime |
| end | query |  | Yes | dateTime |
| interval | query |  | Yes | integer |
| metric | query |  | Yes | integer |
| device_id | query |  | No | [ string ] |
| compare_start | query |  | No | dateTime |
| compare_end | query |  | No | dateTime |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |

### /api/report/adhawk/gender-detail
---
##### ***GET***
**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| start | query |  | Yes | dateTime |
| end | query |  | Yes | dateTime |
| interval | query |  | Yes | integer |
| metric | query |  | Yes | integer |
| device_id | query |  | No | [ string ] |
| compare_start | query |  | No | dateTime |
| compare_end | query |  | No | dateTime |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |

### /api/report/adhawk/device-summary
---
##### ***GET***
**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| start | query |  | Yes | dateTime |
| end | query |  | Yes | dateTime |
| interval | query |  | Yes | integer |
| metric | query |  | Yes | integer |
| device_id | query |  | No | [ string ] |
| compare_start | query |  | No | dateTime |
| compare_end | query |  | No | dateTime |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |

### /api/report/adhawk/device-heatmap
---
##### ***GET***
**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| start | query |  | Yes | dateTime |
| end | query |  | Yes | dateTime |
| interval | query |  | Yes | integer |
| metric | query |  | Yes | integer |
| device_id | query |  | No | [ string ] |
| compare_start | query |  | No | dateTime |
| compare_end | query |  | No | dateTime |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |

### /api/report/adhawk/device-geolocation
---
##### ***GET***
**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| start | query |  | Yes | dateTime |
| end | query |  | Yes | dateTime |
| interval | query |  | Yes | integer |
| metric | query |  | Yes | integer |
| device_id | query |  | No | [ string ] |
| compare_start | query |  | No | dateTime |
| compare_end | query |  | No | dateTime |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |

### /api/report/export/{report_name}
---
##### ***GET***
**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| report_name | path |  | Yes | string |
| format | query |  | No | string |
| activity_type | query |  | No | string |
| interval | query |  | No | string |
| start | query |  | No | dateTime |
| end | query |  | No | dateTime |
| device_id | query |  | No | [ string ] |
| user_id | query |  | No | [ string ] |
| media_id | query |  | No | [ string ] |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |

### /api/schedules
---
##### ***GET***
**Summary:** Gets all schedules in an account.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | query |  | No | string |
| take | query |  | No | integer |
| page | query |  | No | integer |
| group_id | query |  | No | [ string ] |
| group_name | query |  | No | [ string ] |
| device_id | query |  | No | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns an array of schedules | [ [RevelDigital.Core.PublicApi.Models.Schedule](#reveldigital.core.publicapi.models.schedule) ] |

### /api/schedules/{id}
---
##### ***GET***
**Summary:** Gets a schedule by ID.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns the schedule matching the ID | [RevelDigital.Core.PublicApi.Models.Schedule](#reveldigital.core.publicapi.models.schedule) |

##### ***DELETE***
**Summary:** Delete a schedule.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

### /api/schedules/groups
---
##### ***GET***
**Summary:** Gets schedule groups in the account.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | query |  | No | string |
| take | query |  | No | integer |
| page | query |  | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns an array of playlist groups | [ [RevelDigital.Core.PublicApi.Models.Group](#reveldigital.core.publicapi.models.group) ] |

##### ***POST***
**Summary:** Create a new schedule group.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| group | body | Schedule group | No | [RevelDigital.Core.PublicApi.Models.GroupRequest](#reveldigital.core.publicapi.models.grouprequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Returns the newly-created item | [RevelDigital.Core.PublicApi.Models.Group](#reveldigital.core.publicapi.models.group) |
| 400 | If the item is null |

### /api/schedules/groups/{id}
---
##### ***PUT***
**Summary:** Updates a schedule group.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query | API key | No | string |
| id | path | Group id | Yes | string |
| group | body | Device group | No | [RevelDigital.Core.PublicApi.Models.GroupRequest](#reveldigital.core.publicapi.models.grouprequest) |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

##### ***DELETE***
**Summary:** Delete a schedule group.

**Description:** Group must be empty.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

### /api/templates
---
##### ***GET***
**Summary:** Gets all templates in an account.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | query |  | No | string |
| take | query |  | No | integer |
| page | query |  | No | integer |
| group_id | query |  | No | [ string ] |
| group_name | query |  | No | [ string ] |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns an array of templates | [ [RevelDigital.Core.PublicApi.Models.Template](#reveldigital.core.publicapi.models.template) ] |

### /api/templates/{id}
---
##### ***GET***
**Summary:** Gets a template by ID.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns the template matching the ID | [RevelDigital.Core.PublicApi.Models.Template](#reveldigital.core.publicapi.models.template) |

##### ***DELETE***
**Summary:** Delete a template.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

### /api/templates/groups
---
##### ***GET***
**Summary:** Gets template groups in the account.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | query |  | No | string |
| take | query |  | No | integer |
| page | query |  | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns an array of playlist groups | [ [RevelDigital.Core.PublicApi.Models.Group](#reveldigital.core.publicapi.models.group) ] |

##### ***POST***
**Summary:** Create a new template group.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| group | body | Template group | No | [RevelDigital.Core.PublicApi.Models.GroupRequest](#reveldigital.core.publicapi.models.grouprequest) |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Returns the newly-created item | [RevelDigital.Core.PublicApi.Models.Group](#reveldigital.core.publicapi.models.group) |
| 400 | If the item is null |

### /api/templates/groups/{id}
---
##### ***PUT***
**Summary:** Updates a template group.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query | API key | No | string |
| id | path | Group id | Yes | string |
| group | body | Device group | No | [RevelDigital.Core.PublicApi.Models.GroupRequest](#reveldigital.core.publicapi.models.grouprequest) |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

##### ***DELETE***
**Summary:** Delete a template group.

**Description:** Group must be empty.

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Success |
| 400 | Bad Request |

### /api/users
---
##### ***GET***
**Summary:** Gets all users in an account.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | query |  | No | string |
| take | query |  | No | integer |
| page | query |  | No | integer |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns an array of users | [ [RevelDigital.Core.PublicApi.Models.User](#reveldigital.core.publicapi.models.user) ] |

### /api/users/{id}
---
##### ***GET***
**Summary:** Gets a user by ID.

**Description:** 

**Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| api_key | query |  | No | string |
| id | path |  | Yes | string |

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Returns the user matching the ID | [RevelDigital.Core.PublicApi.Models.User](#reveldigital.core.publicapi.models.user) |

### Models
---

### RevelDigital.Core.PublicApi.Models.Account  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| tags | string |  | No |
| business_name | string |  | No |
| address_1 | string |  | No |
| address_2 | string |  | No |
| city | string |  | No |
| state | string |  | No |
| postal_code | string |  | No |
| country | string |  | No |
| phone | string |  | No |
| fax | string |  | No |
| primary_contact_id | string |  | No |
| secondary_contact_id | string |  | No |
| created_on | string |  | No |
| timezone | string |  | No |
| logo_url | string |  | No |

### RevelDigital.Core.PublicApi.Models.Device  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| group_name | string |  | No |
| group_id | string |  | No |
| tags | string |  | No |
| device_type | [RevelDigital.Core.PublicApi.Models.DeviceType](#reveldigital.core.publicapi.models.devicetype) |  | No |
| entered_service | string |  | No |
| last_service | string |  | No |
| timezone | string |  | No |
| last_update | string |  | No |
| location | [RevelDigital.Core.PublicApi.Models.Location](#reveldigital.core.publicapi.models.location) |  | No |
| ping_data | [RevelDigital.Core.PublicApi.Models.PingData](#reveldigital.core.publicapi.models.pingdata) |  | No |
| registration_key | string |  | No |
| mac_address | string |  | No |
| beacon | [RevelDigital.Core.PublicApi.Models.Beacon](#reveldigital.core.publicapi.models.beacon) |  | No |

### RevelDigital.Core.PublicApi.Models.DeviceType  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| manufacturer | string |  | No |
| device_caps | integer |  | No |

### RevelDigital.Core.PublicApi.Models.Location  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| city | string |  | No |
| state | string |  | No |
| county | string |  | No |
| country | string |  | No |
| postal_code | string |  | No |
| address | string |  | No |
| latitude | double |  | No |
| longitude | double |  | No |

### RevelDigital.Core.PublicApi.Models.PingData  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| snap | byte |  | No |
| player_version | string |  | No |
| os_version | string |  | No |
| cpu_usage | float |  | No |
| memory_usage | float |  | No |
| mac_address | string |  | No |
| disk_usage | float |  | No |
| timestamp | dateTime |  | No |
| bytes_received | long |  | No |
| transfer_rate | long |  | No |
| ip_address | string |  | No |
| latitude | double |  | No |
| longitude | double |  | No |

### RevelDigital.Core.PublicApi.Models.Beacon  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| distance | double |  | No |
| calibration | double |  | No |
| phone | string |  | No |
| email | string |  | No |
| website | string |  | No |
| devices | [ string ] |  | No |
| rating | double |  | No |
| uuid | string |  | No |
| major | string |  | No |
| minor | string |  | No |
| notification_delay | integer |  | No |
| instance_id | string |  | No |
| namespace | string |  | No |

### RevelDigital.Core.PublicApi.Models.DeviceRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string |  | Yes |
| tags | string |  | No |
| timezone | string |  | No |
| group_id | string |  | No |
| last_service | dateTime |  | No |
| mac_address | string |  | No |
| location | [RevelDigital.Core.PublicApi.Models.Location](#reveldigital.core.publicapi.models.location) |  | No |
| beacon | [RevelDigital.Core.PublicApi.Models.Beacon](#reveldigital.core.publicapi.models.beacon) |  | No |

### RevelDigital.Core.PublicApi.Models.Group  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |

### RevelDigital.Core.PublicApi.Models.GroupRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string |  | No |

### RevelDigital.Core.PublicApi.Models.DeviceCommand  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| device_id | string |  | No |
| commands | [ [RevelDigital.Core.PublicApi.Models.Command](#reveldigital.core.publicapi.models.command) ] |  | No |

### RevelDigital.Core.PublicApi.Models.Command  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string |  | No |
| arg | string |  | No |

### RevelDigital.Core.PublicApi.Models.Media  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| group_name | string |  | No |
| group_id | string |  | No |
| tags | string |  | No |
| mime_type | string |  | No |
| file_size | integer |  | No |
| file_name | string |  | No |
| file_url | string |  | No |
| thumbnail_url | string |  | No |
| uploaded_on | string |  | No |
| uploaded_by | string |  | No |
| advertiser_id | string |  | No |
| is_shared | boolean |  | No |
| start_date | string |  | No |
| end_date | string |  | No |

### RevelDigital.Core.PublicApi.Models.MediaRequest  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string |  | No |
| group_id | string |  | No |
| tags | string |  | No |
| advertiser_id | string |  | No |
| is_shared | boolean |  | No |
| start_date | dateTime |  | No |
| end_date | dateTime |  | No |

### RevelDigital.Core.PublicApi.Models.Playlist  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| group_name | string |  | No |
| group_id | string |  | No |
| tags | string |  | No |
| type | string |  | No |
| created_on | string |  | No |
| created_by_id | string |  | No |
| modified_on | string |  | No |
| modified_by_id | string |  | No |
| sources | [ [RevelDigital.Core.PublicApi.Models.Source](#reveldigital.core.publicapi.models.source) ] |  | No |

### RevelDigital.Core.PublicApi.Models.Source  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| type | string |  | No |
| sequence | integer |  | No |
| media_id | string |  | No |
| template_id | string |  | No |
| value | string |  | No |
| interval | integer |  | No |
| media | [RevelDigital.Core.PublicApi.Models.Media](#reveldigital.core.publicapi.models.media) |  | No |
| conditions | [ [RevelDigital.Core.PublicApi.Models.Condition](#reveldigital.core.publicapi.models.condition) ] |  | No |

### RevelDigital.Core.PublicApi.Models.Condition  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| type | string |  | No |
| operator | integer |  | No |
| value_1 | string |  | No |
| value_2 | string |  | No |
| value_3 | string |  | No |
| value_4 | string |  | No |

### RevelDigital.Core.PublicApi.Models.Schedule  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| group_name | string |  | No |
| group_id | string |  | No |
| tags | string |  | No |
| monday | boolean |  | No |
| tuesday | boolean |  | No |
| wednesday | boolean |  | No |
| thursday | boolean |  | No |
| friday | boolean |  | No |
| saturday | boolean |  | No |
| sunday | boolean |  | No |
| start_time | string |  | No |
| end_time | string |  | No |
| template_id | string |  | No |
| playlist_id | string |  | No |
| type | string |  | No |
| start_date | string |  | No |
| end_date | string |  | No |
| devices | [ [RevelDigital.Core.PublicApi.Models.ScheduleDevice](#reveldigital.core.publicapi.models.scheduledevice) ] |  | No |
| conditions | [ [RevelDigital.Core.PublicApi.Models.Condition](#reveldigital.core.publicapi.models.condition) ] |  | No |

### RevelDigital.Core.PublicApi.Models.ScheduleDevice  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |

### RevelDigital.Core.PublicApi.Models.Template  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| group_name | string |  | No |
| group_id | string |  | No |
| tags | string |  | No |
| created_on | string |  | No |
| created_by_id | string |  | No |
| modified_on | string |  | No |
| modified_by_id | string |  | No |
| script | string |  | No |
| back_color | string |  | No |
| width | integer |  | No |
| height | integer |  | No |
| orientation | integer |  | No |
| modules | [ [RevelDigital.Core.PublicApi.Models.Module](#reveldigital.core.publicapi.models.module) ] |  | No |

### RevelDigital.Core.PublicApi.Models.Module  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| name | string |  | No |
| type | string |  | No |
| left | integer |  | No |
| top | integer |  | No |
| width | integer |  | No |
| height | integer |  | No |
| playlist_id | string |  | No |
| sequence | integer |  | No |

### RevelDigital.Core.PublicApi.Models.User  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string |  | No |
| first_name | string |  | No |
| last_name | string |  | No |
| city | string |  | No |
| state | string |  | No |
| postal_code | string |  | No |
| country | string |  | No |
| home_phone | string |  | No |
| work_phone | string |  | No |
| mobile_phone | string |  | No |
| created_on | string |  | No |
| email | string |  | Yes |
| role | [ string ] |  | Yes |
| user_name | string |  | Yes |
| last_activity | string |  | No |