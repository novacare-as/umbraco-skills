# Language — API Endpoints

See `schemas/language.md` for field definitions.

## Contents

### Language

- `GET /umbraco/management/api/v1/item/language`
- `GET /umbraco/management/api/v1/item/language/default`
- `GET /umbraco/management/api/v1/language`
- `POST /umbraco/management/api/v1/language`
- `GET /umbraco/management/api/v1/language/{isoCode}`
- `DELETE /umbraco/management/api/v1/language/{isoCode}`
- `PUT /umbraco/management/api/v1/language/{isoCode}`

---

## Language

### `GET /umbraco/management/api/v1/item/language`

**Gets a collection of language items.**

Operation ID: `GetItemLanguage`

| Param | In | Type | Required |
|-------|----|------|----------|
| `isoCode` | query | List<string> | No |

**Response 200:** `List<object>`

---

### `GET /umbraco/management/api/v1/item/language/default`

**Gets the default language.**

Operation ID: `GetItemLanguageDefault`

**Response 200:** `OneOf: → LanguageItemResponseModel`

---

### `GET /umbraco/management/api/v1/language`

**Gets a paginated collection of languages.**

Operation ID: `GetLanguage`

| Param | In | Type | Required |
|-------|----|------|----------|
| `skip` | query | integer (int32) | No |
| `take` | query | integer (int32) | No |

**Response 200:** `OneOf: → PagedLanguageResponseModel`

---

### `POST /umbraco/management/api/v1/language`

**Creates a new language.**

Operation ID: `PostLanguage`

**Request body:** `OneOf: → CreateLanguageRequestModel`


---

### `GET /umbraco/management/api/v1/language/{isoCode}`

**Gets a language by ISO code.**

Operation ID: `GetLanguageByIsoCode`

| Param | In | Type | Required |
|-------|----|------|----------|
| `isoCode` | path | string | Yes |

**Response 200:** `OneOf: → LanguageResponseModel`

---

### `DELETE /umbraco/management/api/v1/language/{isoCode}`

**Deletes a language.**

Operation ID: `DeleteLanguageByIsoCode`

| Param | In | Type | Required |
|-------|----|------|----------|
| `isoCode` | path | string | Yes |


---

### `PUT /umbraco/management/api/v1/language/{isoCode}`

**Updates a language.**

Operation ID: `PutLanguageByIsoCode`

| Param | In | Type | Required |
|-------|----|------|----------|
| `isoCode` | path | string | Yes |

**Request body:** `OneOf: → UpdateLanguageRequestModel`


---
