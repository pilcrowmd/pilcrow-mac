---
service: tidewatch
owner: harbour-team
on_call: "#harbour-oncall"
last_review: 2026-09-30
severity_levels: [SEV1, SEV2, SEV3]
---

# Runbook: tidewatch database connections

> [!CAUTION]
> If readings have stopped for more than 15 minutes, treat it as **SEV1**. The harbour office
> has no other live water level.

## When to use this runbook

Use it when you see any of these alerts:

| Alert | Fires when | Severity |
|:--|:--|:--:|
| `TidewatchNoReadings` | No new reading for 10 minutes | SEV1 |
| `TidewatchDbPoolFull` | Pool use above 90% for 5 minutes | SEV2 |
| `TidewatchSlowQueries` | p95 query time above 500 ms | SEV3 |

## 1. Check the service

```bash
kubectl -n harbour get pods -l app=tidewatch
kubectl -n harbour logs deploy/tidewatch --since=15m | grep -i -E "error|timeout"
```

Healthy output shows every pod as `Running` with `READY 1/1`.

> [!IMPORTANT]
> Do not restart pods before you have saved the logs. A restart removes the evidence.

```bash
kubectl -n harbour logs deploy/tidewatch --since=1h > tidewatch-$(date +%F-%H%M).log
```

## 2. Check the connection pool

```sql
SELECT state, count(*)
FROM pg_stat_activity
WHERE datname = 'tidewatch'
GROUP BY state
ORDER BY count(*) DESC;
```

| State | Normal | Problem |
|:--|--:|--:|
| `active` | 2–8 | more than 40 |
| `idle` | 5–20 | – |
| `idle in transaction` | 0 | any |

## 3. Fix

- **Pool full, many `idle in transaction`:** a client is not closing transactions. Restart that
  client, not the database.
- **Pool full, many `active`:** a slow query is blocking. Find it:

```sql
SELECT pid, now() - query_start AS running_for, left(query, 80) AS query
FROM pg_stat_activity
WHERE state = 'active'
ORDER BY running_for DESC
LIMIT 5;
```

- **Gauge unreachable:** check the gauge from inside the cluster:

```bash
kubectl -n harbour exec deploy/tidewatch -- curl -s -m 5 "$GAUGE_NORTH_URL/status"
```

## 4. Settings that matter

```yaml
database:
  pool_size: 20
  pool_timeout: 10s
  statement_timeout: 30s
  idle_in_transaction_timeout: 60s
```

> [!WARNING]
> `pool_size` × replicas must stay below the database limit of 100 connections. With 4
> replicas, the maximum safe `pool_size` is 24.

## 5. After the incident

- [ ] Post a short summary in `#harbour-oncall`
- [ ] Add the timeline to the incident log
- [ ] Open a ticket for any fix that is not done yet
- [ ] Book a 30-minute review within 5 working days

<details>
<summary>Incident 2026-09-12 – what happened last time</summary>

| Time (UTC) | Event |
|:--|:--|
| 03:12 | `TidewatchDbPoolFull` fired |
| 03:19 | On-call found 38 connections `idle in transaction` |
| 03:24 | The report job was restarted; pool back to normal |
| 03:40 | Readings confirmed for all four gauges |

**Cause:** the nightly report job opened a transaction and waited on a slow export.
**Fix:** `idle_in_transaction_timeout` set to 60 s.

</details>

## Contacts

| Role | Who | How |
|:--|:--|:--|
| Primary on-call | rota | `#harbour-oncall` |
| Database owner | platform team | `#platform` |
| Harbour office | duty officer | phone list in the office wiki |

## Open follow-ups

- Add a limit check so the total pool across replicas cannot exceed the database maximum.
- Lower the first alert threshold from 10 minutes to 3.
- Review this runbook with the next on-call group.
