

### 2. Check dependency latency (MOST IMPORTANT)

## Latency without errors usually means:

<!-- IMP:  DNS delay > External API slow > Cache misses > Connection pool exhaustion > Database slow -->

* DNS delay
* External API slow
* Cache misses
* Connection pool exhaustion
* Database slow

## What to check:

* DB query p95 latency
* Redis hit/miss ratio
* External API response time
* Connection pool usage
---


#### Scope the blast radius

```text
- One endpoint or all?
- One AZ(avialabtlity Zone) or all?
- One pod or all replicas?
```

How:

* APM (Grafana / Datadog / NewRelic)
* Per-endpoint latency dashboards
---

#### Check saturation signals (not CPU)

SRE golden signals:

* **1. Latency**
* **2. Traffic**
* **3. Errors**
* **4. Saturation**


> Here, saturation might be:
> ##### Saturation Signals: 
>   * DB connections maxed
>   * Thread pool exhausted
>   * Queue depth increasing

---
