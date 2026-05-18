# Telemetry Schemas

## Schemas in this file

- [PagedTelemetryResponseModel](#pagedtelemetryresponsemodel)
- [TelemetryLevelModel](#telemetrylevelmodel)
- [TelemetryRequestModel](#telemetryrequestmodel)
- [TelemetryResponseModel](#telemetryresponsemodel)

---

## PagedTelemetryResponseModel

**Fields:**

- `items`: List<object> **required**
- `total`: integer (int64) **required**

---

## TelemetryLevelModel

**Enum values:** `Minimal`, `Basic`, `Detailed`

---

## TelemetryRequestModel

**Fields:**

- `telemetryLevel`: → `TelemetryLevelModel` **required**

---

## TelemetryResponseModel

**Fields:**

- `telemetryLevel`: → `TelemetryLevelModel` **required**

---
