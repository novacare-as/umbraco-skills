# Log Viewer — API Endpoints

See `schemas/log-viewer.md` for field definitions.

## Contents

### Log Viewer

- `GET /umbraco/management/api/v1/log-viewer/level`
- `GET /umbraco/management/api/v1/log-viewer/level-count`
- `GET /umbraco/management/api/v1/log-viewer/log`
- `GET /umbraco/management/api/v1/log-viewer/message-template`
- `GET /umbraco/management/api/v1/log-viewer/saved-search`
- `POST /umbraco/management/api/v1/log-viewer/saved-search`
- `GET /umbraco/management/api/v1/log-viewer/saved-search/{name}`
- `DELETE /umbraco/management/api/v1/log-viewer/saved-search/{name}`
- `GET /umbraco/management/api/v1/log-viewer/validate-logs-size`

---

## Log Viewer

### `GET /umbraco/management/api/v1/log-viewer/level`

**Gets a collection of log sink levels.**

Operation ID: `GetLogViewerLevel`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedLoggerResponseModel`

---

### `GET /umbraco/management/api/v1/log-viewer/level-count`

**Gets log level counts.**

Operation ID: `GetLogViewerLevelCount`

| Param | In | Type | Required |
|-------|----|------|----------|
| `startDate` | query | string (date-time) | No |
| `endDate` | query | string (date-time) | No |

**Response 200:** `OneOf: → LogLevelCountsReponseModel`

---

### `GET /umbraco/management/api/v1/log-viewer/log`

**Gets a paginated collection of log entries.**

Operation ID: `GetLogViewerLog`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `orderDirection` | query | → DirectionModel | No |
| `filterExpression` | query | string | No |
| `logLevel` | query | List<`LogLevelModel`> | No |
| `startDate` | query | string (date-time) | No |
| `endDate` | query | string (date-time) | No |

**Response 200:** `OneOf: → PagedLogMessageResponseModel`

---

### `GET /umbraco/management/api/v1/log-viewer/message-template`

**Gets a collection of log message templates.**

Operation ID: `GetLogViewerMessageTemplate`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |
| `startDate` | query | string (date-time) | No |
| `endDate` | query | string (date-time) | No |

**Response 200:** `OneOf: → PagedLogTemplateResponseModel`

---

### `GET /umbraco/management/api/v1/log-viewer/saved-search`

**Gets a collection of saved log searches.**

Operation ID: `GetLogViewerSavedSearch`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedSavedLogSearchResponseModel`

---

### `POST /umbraco/management/api/v1/log-viewer/saved-search`

**Creates a saved log search.**

Operation ID: `PostLogViewerSavedSearch`

**Request body:** `OneOf: → SavedLogSearchRequestModel`


---

### `GET /umbraco/management/api/v1/log-viewer/saved-search/{name}`

**Gets a saved log search by name.**

Operation ID: `GetLogViewerSavedSearchByName`

| Param | In | Type | Required |
|-------|----|------|----------|
| `name` | path | string | Yes |

**Response 200:** `OneOf: → SavedLogSearchResponseModel`

---

### `DELETE /umbraco/management/api/v1/log-viewer/saved-search/{name}`

**Deletes a saved log search.**

Operation ID: `DeleteLogViewerSavedSearchByName`

| Param | In | Type | Required |
|-------|----|------|----------|
| `name` | path | string | Yes |


---

### `GET /umbraco/management/api/v1/log-viewer/validate-logs-size`

**Validates if logs can be viewed.**

Operation ID: `GetLogViewerValidateLogsSize`

| Param | In | Type | Required |
|-------|----|------|----------|
| `startDate` | query | string (date-time) | No |
| `endDate` | query | string (date-time) | No |


---
