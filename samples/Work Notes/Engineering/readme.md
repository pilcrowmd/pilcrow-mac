---
project: tidewatch
version: 2.4.0
license: MIT
maintainers: [harbour-team]
---

# tidewatch

A small service that reads tide gauges, stores the readings, and warns the harbour office
before the water gets too high or too low.

> [!NOTE]
> This README is a demo file for PilcrowMD. The project is invented.

## Contents

- [Quick start](#quick-start)
- [Configuration](#configuration)
- [API](#api)
- [Clients](#clients)
- [Database](#database)
- [Roadmap](#roadmap)

## Quick start

```bash
git clone https://example.com/harbour/tidewatch.git
cd tidewatch
make setup        # installs tools and creates .env
make run          # starts the service on port 8080
```

Check that it is alive:

```bash
curl -s http://localhost:8080/health | jq .
```

```json
{
  "status": "ok",
  "gauges": 4,
  "last_reading": "2026-10-07T06:40:00Z"
}
```

> [!TIP]
> Run `make test` before every push. It takes about 40 seconds.

## Configuration

All settings live in one file. Values in `${...}` come from the environment.

```yaml
server:
  port: 8080
  read_timeout: 5s
gauges:
  - id: north-pier
    url: ${GAUGE_NORTH_URL}
    poll_every: 60s
  - id: south-basin
    url: ${GAUGE_SOUTH_URL}
    poll_every: 60s
alerts:
  high_water_m: 4.20
  low_water_m: 0.35
```

| Setting | Default | What it does |
|:--|:--:|:--|
| `server.port` | `8080` | Port for the HTTP API |
| `poll_every` | `60s` | How often each gauge is read |
| `high_water_m` | `4.20` | Level that sends a high-water alert |
| `low_water_m` | `0.35` | Level that sends a low-water alert |

## API

| Method | Path | Returns |
|:--|:--|:--|
| `GET` | `/health` | Service status |
| `GET` | `/gauges` | All gauges and their last reading |
| `GET` | `/gauges/{id}/readings?from=…&to=…` | Readings for one gauge |
| `POST` | `/alerts/test` | Sends a test alert |

## Clients

The reading model is the same in every client.

```python
from dataclasses import dataclass
from datetime import datetime

@dataclass
class Reading:
    gauge_id: str
    level_m: float
    taken_at: datetime

    def is_high(self, limit: float = 4.20) -> bool:
        return self.level_m >= limit
```

```typescript
interface Reading {
  gaugeId: string;
  levelM: number;
  takenAt: string; // ISO 8601
}

export async function latest(gaugeId: string): Promise<Reading> {
  const res = await fetch(`/gauges/${gaugeId}/readings?limit=1`);
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return (await res.json())[0];
}
```

```kotlin
data class Reading(
    val gaugeId: String,
    val levelM: Double,
    val takenAt: Instant,
) {
    fun isHigh(limit: Double = 4.20) = levelM >= limit
}
```

```swift
struct Reading: Codable {
    let gaugeId: String
    let levelM: Double
    let takenAt: Date

    func isHigh(limit: Double = 4.20) -> Bool { levelM >= limit }
}
```

```go
type Reading struct {
	GaugeID string    `json:"gauge_id"`
	LevelM  float64   `json:"level_m"`
	TakenAt time.Time `json:"taken_at"`
}

func (r Reading) IsHigh(limit float64) bool { return r.LevelM >= limit }
```

```rust
pub struct Reading {
    pub gauge_id: String,
    pub level_m: f64,
    pub taken_at: chrono::DateTime<chrono::Utc>,
}

impl Reading {
    pub fn is_high(&self, limit: f64) -> bool {
        self.level_m >= limit
    }
}
```

## Database

```sql
CREATE TABLE readings (
    gauge_id  TEXT        NOT NULL,
    level_m   REAL        NOT NULL,
    taken_at  TIMESTAMPTZ NOT NULL,
    PRIMARY KEY (gauge_id, taken_at)
);

-- Highest level per gauge in the last 24 hours
SELECT gauge_id, MAX(level_m) AS peak_m
FROM readings
WHERE taken_at > now() - INTERVAL '24 hours'
GROUP BY gauge_id
ORDER BY peak_m DESC;
```

> [!WARNING]
> Never run migrations against production by hand. Use `make migrate ENV=prod`, which takes
> a backup first.

<details>
<summary>Why readings are stored in metres, not centimetres</summary>

The harbour office reports in metres with two decimals. Storing the same unit avoids a
conversion step in every report and every alert message.

</details>

## Roadmap

- [x] Read four gauges every minute
- [x] High- and low-water alerts by email
- [x] Health endpoint for the monitoring system
- [ ] SMS alerts for the night shift
- [ ] A seven-day forecast from the tide tables[^tables]
- [ ] Dashboard for the harbour office

## Contributing

1. Open an issue first, so we agree on the change.
2. Keep pull requests small – one change each.
3. Add a test for every bug you fix.

[^tables]: The tide tables are published once a year by the port authority.
