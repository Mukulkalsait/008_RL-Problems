

### 2. Check dependency latency (MOST IMPORTANT)

## Latency without errors usually means:

<!-- IMP:  DNS delay > External API slow > Cache misses > Connection pool exhaustion > Database slow -->

* DNS delay
* External API slow
* Cache misses
* Connection pool exhaustion
* Database slow

- additions added by me:
  some other I/O slow? 
  Thread block?

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

#### Check retries & timeouts

Silent latency killer:

* Retry storms
* Missing timeouts
* Long backoff policies

---

## 3️⃣ Mitigation (SAFE, SRE-style)

### Short-term

* Increase connection pool (if safe)
* Reduce retries
* Temporarily disable slow dependency
* Serve stale cache / fallback response

### 5️⃣ Post-Incident / Prevention (YOU MUST HAVE THIS)

* Examples you could say:

    -  Add per-dependency latency SLOs
    -  Enforce timeouts + circuit breakers
    -  Alert on p95 dependency latency
    -  Load test with slow-dependency scenarios
    -  Improve dashboards for saturation signals
    -  Even 2 of these would’ve boosted your score to 7+.

