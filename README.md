# Air Quality Data Client API (discussion)

## Challenges

- Mobile device internet connection is often slow and can change rapidly during usage.
- Mobile devices are constrained by battery energy capacity.

## STANDARDS

### Pollutants and their measurement units

- Carbon Monoxide - Concentration, unit: **mg/m³**
- Lead - Concentration, unit: **µg/m³**
- Nitrogen Dioxide - Concentration, unit: **µg/m³**
- Ozone - Concentration, unit: **µg/m³**
- Particulate Matter (PM10) - Concentration, unit: **µg/m³**
- Particulate Matter (PM2.5) - Concentration, unit: **µg/m³**
- Sulfur Dioxide - Concentration, unit: **µg/m³**

## Protocol

Here `HTTP/1.1` will be used.

### Secure Transport

- Secure Sockets Layer version 3.0 (SSLv3)
- Transport Layer Security (TLS) versions 1.0 through 1.2

For Apple platforms see: [Secure Transport](https://developer.apple.com/reference/security/secure_transport)

## Authorization

Before you can use the REST API, you must have an `SECRET` key for your app, generated per `APPID` (iOS: Bundle ID, Android: package) for.

It will be used for client identification and per app traffic throttling if necessary.

We use [OAuth 2.0](https://tools.ietf.org/html/rfc6749) for client authorization.

### OAuth 2.0 Flow

Client credentials grant ([section 4.4](https://tools.ietf.org/html/rfc6749#section-4.4)).

`POST /v1/token`

#### Headers:

`Authorization: Basic APPID:SECRET`

#### Payload (application/x-www-form-urlencoded):

```
grant_type=client_credentials
```

#### Responses:

**Success:**

Status 200, (application/json):

```json
{
	"token_type": "bearer",
	"expires_in": 3600,
	"access_token": "ACCESS_TOKEN"
}
```

**Failure:**

If the request failed client authentication or is invalid, the authorization server returns an error response as described in [Section 5.2](https://tools.ietf.org/html/rfc6749#section-5.2).

## Air Quality Request

`GET /v1/quality`

#### Headers:

`Authorization: Bearer ACCESS_TOKEN`

#### Parameters (application/x-www-form-urlencoded):

```
latitude=0.0&longitude=0.0
```

#### Responses:

**Success:**

Status 200, (application/json):

```json
{
	"distance": 1000.0,
	"timestamp": 1234567,
	"assessment": 0.1,
	"PM10": {"measured": 203.0, "norm": 34.0}
}
```

- **distance** (float) - distance to closest sensor in meters
- **timestamp** (integer) - oldest pollutant reading UNIX TIMESTAMP GMT+0000
- **assessment** (float) - 0.0 - 1.0 where 0.0 means stay at home and 1.0 is an air pollution within european norm. Can be `null` if the reading is too far and cannot be used for assessment.
- **pollutants, example PM10** (object) - list of pollutant readings with their respective european maximum norms.
