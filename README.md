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

### 