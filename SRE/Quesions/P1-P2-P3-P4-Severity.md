
## Q1️⃣ What is P1, P2, P3 severity?

### 🔥 P1 – Critical

* User-facing outage
* Revenue or core feature impacted
* PagerDuty wakes people at night

**Examples**

* Payments down
* Login broken
* API OOMKilled repeatedly

---

### ⚠️ P2 – High

* Partial impact
* Degraded performance
* No full outage

**Examples**

* High latency
* Some users failing
* One AZ affected

---

### 🟡 P3 – Medium

* No immediate user impact
* Needs fixing but not urgent

**Examples**

* Disk usage rising slowly
* Node nearing capacity
* Backup delay

---

### 🟢 P4 – Low

* Informational
* Maintenance / hygiene

**Examples**

* SSL expiry in 30 days
* Cron failure (non-critical)

👉 **Rule**:
If users notice → P1 or P2
If only engineers notice → P3/P4

---
