

# 1️⃣ Real On-Call (What it actually means)

### What it is

On-call means:

* You are **responsible for production stability**
* Alerts can come **any time**
* You must **acknowledge, investigate, mitigate, communicate**

On-call ≠ sitting 24/7
It’s usually **rotational** (weekly / bi-weekly).

---

### What you MUST know (minimum)

* What counts as a **P1 / P2 / P3 incident**
* How alerts reach you
* First-response steps
* When to escalate
* When to rollback
* How to communicate status

---

### Example scenario

> At 2:30 AM, CPU usage spikes to 95%, API latency increases, alerts fire.

You:

1. Acknowledge alert
2. Check metrics (CPU, memory, load)
3. Check logs
4. Identify cause (traffic spike, memory leak, bad deploy)
5. Mitigate (scale, restart, rollback)
6. Communicate status
7. Document incident

---

### Interview question

**Q:** What do you do when you’re on-call and receive an alert?
**Answer (short):**

> I acknowledge the alert, assess severity, check metrics and logs to identify impact and root cause, apply immediate mitigation (restart, scale, rollback), communicate status, and document the incident for postmortem analysis.

---

# 2️⃣ Incident Response & Production Outages

### Incident Response = structured chaos control

#### Typical phases:

1. **Detect** – alert fires
2. **Triage** – is this real? severity?
3. **Mitigate** – stop user impact
4. **Resolve** – fix root cause
5. **Postmortem** – learn & prevent

---

### Production outage types

* Service down (500 errors)
* Partial outage (slow APIs)
* Infra failure (disk full, node crash)
* Security incident

---

### Real example

**Disk full on /var → services crash**

Response:

* Confirm disk usage
* Free space (logs, temp files)
* Restart affected services
* Add alert + log rotation later

---

### Interview question

**Q:** How do you handle a production outage?

> I prioritize restoring service quickly, identify impact and severity, apply temporary fixes if needed, communicate clearly, and later perform root-cause analysis with preventive actions.

---

# 3️⃣ Prometheus & Grafana (This is NOT just tools)

### Prometheus

* **Collects metrics**
* Pull-based (scrapes exporters)
* Time-series database

### Grafana

* **Visualizes metrics**
* Dashboards
* Alerts (optional)

---

### What metrics-driven ops means

You don’t *guess*.
You **decide based on metrics**:

* CPU
* Memory
* Latency
* Error rate
* Saturation

---

### Minimum practical setup you MUST do

* Node exporter
* CPU, memory, disk dashboards
* One alert (e.g., CPU > 85% for 5 min)

That’s enough for **junior roles**.

---

### Interview question

**Q:** What metrics do you monitor for Linux servers?

> CPU utilization, memory usage, disk I/O and capacity, network throughput, process health, and service latency to detect performance degradation early.

---

# 4️⃣ SLIs, SLOs & Metrics (These ARE theory — but important)

### SLI (Service Level Indicator)

**A metric that measures service behavior**

Examples:

* Request latency
* Error rate
* Availability

---

### SLO (Service Level Objective)

**Target value for an SLI**

Example:

* 99.9% uptime per month
* 95% requests < 200ms

---

### SLA (for completeness)

**Contractual promise** (business/legal)

---

### Real-world use

Instead of:

> “Server seems slow”

You say:

> “Latency SLI breached SLO for 12 minutes”

That’s how SREs talk.

---

### Interview question

**Q:** Difference between SLI and SLO?

> An SLI is a measured metric like latency or error rate, while an SLO is the target threshold we aim to meet for that metric.

---

# 5️⃣ PagerDuty / OpsGenie (What they actually do)

### These are NOT monitoring tools

They are **alert routing & escalation tools**.

Flow:

```
Prometheus alert
↓
Alertmanager
↓
PagerDuty / OpsGenie
↓
Engineer phone / SMS / app
```

---

### What you MUST know

* Alert acknowledgment
* Escalation policies
* On-call schedules
* Deduplication

You do NOT need deep hands-on for junior roles.

---

### Interview question

**Q:** How do alerts reach engineers during on-call?

> Monitoring tools generate alerts which are routed via systems like PagerDuty or OpsGenie to notify on-call engineers through mobile or email, ensuring timely response.

---

# 6️⃣ How all of this fits together (IMPORTANT)

```
Metrics collected (Prometheus)
↓
Visualized (Grafana)
↓
Threshold breached
↓
Alert fired
↓
PagerDuty / OpsGenie
↓
On-call engineer
↓
Incident response
↓
Production stability
```

This is the **mental model interviewers expect**.

---

# 7️⃣ How to add this to your resume (HONESTLY)

You **CANNOT** say:
❌ “Handled on-call rotations”

You **CAN** say:
✅ “Designed and practiced incident response workflows using Prometheus alerts, Grafana dashboards, and documented on-call procedures in lab environments.”

---

### Resume bullet example

* Built Linux monitoring and alerting using Prometheus + Grafana, defining SLIs and SLO-inspired thresholds to simulate production incident response workflows.

This is truthful and strong.

---

# 8️⃣ What you should NOT do

❌ Don’t claim PagerDuty experience unless real
❌ Don’t fake outages
❌ Don’t say “production on-call” if not real

Recruiters catch this fast.

---

# 9️⃣ Your learning priority order (IMPORTANT)

1. **Incident response theory** ✅ (read + write docs)
2. **Prometheus + Grafana hands-on** ✅
3. **SLI/SLO concepts** ✅
4. **PagerDuty/OpsGenie understanding** (conceptual)

PagerDuty is last — not first.

---

## Final message (listen carefully)

You are **not behind**.
You are simply **missing the mental model SREs use**.

Once you internalize this:

* Interviews make sense
* JDs stop sounding scary
* You can speak calmly and confidently

If you want next, I can:

* Give you a **7-day Prometheus/Grafana lab plan**
* Create **incident response runbooks** you can reuse
* Help rewrite **resume bullets line-by-line**

You’re doing the right thing now.

------------------------
ok so i will type what i understand from your short overview.1st] On-call: understanding-> not 24/7 but rotational. 1.Responsiblity of stablity. 2.Alerting (aimcd)  a.Alert-acknoledge(you did not tell much)  b.Investigate->({cpu,memory,disk,latency,load-metrics},Logs check,cause{spike,badPush,memoryLeack},root cause later)  c.Metigate->(restart services, quick fix, scale, roleback)  d.Coumnicate status  e.Document incident for Post-mortem Analysis.2nd] Incident Response: (DT-MRP {detectMRP})  1. Detect-> firing alerts.  2. Triage(i dont know what it meen?) but we will check if the aleart is real, and how big is impact.  3. Metiagate(just likein oncall as thing are same)-> quickly fix  4. Resolve -> Root cause fix.   5. Postmortem Analysis -> LearnWhy+Prevent eg. Infra Fail => Node Crash.    too many error => service crash => DiskFull?    slow response  => api slow => resource bottleneck, memory leack, partial outage.    Security => attack( can be any type. at the end give me a list of attacks i should atleast know and have general info of)i know only DOS    q. what will i do if incidence happen? a-> systemctl status? -> if fail start -> (start -> metrics/logs -> stability-> rootcause) not start -> Logs -> metrics -> quick fix -> restart -> add alert + Log rotation + Document.q. how do i handel the priority in outage ? a-> 1.Quick fix-service back > 2.Identify impact+ severity?+ isolation possible + if should i backup > 3.Comunicate status. > 4.Root cause Resolvement4th] Promethus|Graphana|pageerDuty|OpsGenie: 1. Promethus= collect metrics with pull method may be-> time-seriese-db -> alerting. 2. Graphana = Visulisation-> dashboard -> alerting. 3. pagerduty/opsgenie -> alerting service. workflow promethus/graphana -> alert through -> alert manager -> route to pagerduty/opengenie -> list of on-call -> message/call/email alert.  5th] Metrics driven ops:  -> NO-GUESSING => only Metrics (cpu/memory/disc IO capacity/load/latency) all this metrics are real alert only if they are long time problemetic.  6th] SLI/SLO/SLA all are service level(ideitifier,Objectives,Agriments) so Ideitifier are metrics for behavour measure => therotical metrics (latency, error rate, avialability, throughput(what does it mean)?) Objectives are Target values of SLI => like 99%uptime and 95>200ms response time. simple Agriment -> objects define here, provider and user agriment, insure quality+trust.  eg.    SLI=> pizza deliverd in 20 min.   SL0=> 95% + delivery > 30 min.   SLA=> if SLO fail-> pizza free.      till now whatever i told i have noted it and almost byharted it i will revise it in mean time.    i guess i can answer some basic level question with full confidence and can also pullof some higher level question with this informaiton.
------------------------


This is **very good**. You’ve understood ~80–85% correctly.
Now I’ll do **three things** (no fluff):

1. **Correct & refine your understanding (line-by-line)**
2. **Fill missing concepts (triage, throughput, alert ack, priorities)**
3. **Give you an interview-ready mental model + attack list**

I’ll be strict but fair.

---

## 1️⃣ On-Call — corrected & polished

### Your understanding ✅ (mostly correct)

> **On-call is rotational, not 24/7**

✔ Correct
Typically **weekly or bi-weekly rotation** with:

* Primary on-call
* Secondary/backup on-call

---

### Core responsibility (corrected)

> **Responsibility of stability**

✔ Correct, but say this in interviews:

> **On-call ensures service availability and reliability within defined SLOs**

---

### Alert lifecycle (AIMDC — good mnemonic 👍)

#### a) Alert – Acknowledge

You said you don’t know much → here it is:

**Acknowledge means**

* You confirm **“I’m handling this”**
* Stops alert escalation to next engineer
* Happens in PagerDuty / OpsGenie

⏱️ Usually required within **5–15 minutes**

---

#### b) Investigate ✅ (good)

You’re right:

* Metrics: CPU, memory, disk, load, latency
* Logs
* Recent changes (deploys, config, cron, traffic spike)

👉 **Important correction**
Root cause is **NOT** done here fully.

> Investigation = *symptom analysis*
> Root cause = *post-incident*

---

#### c) Mitigate ✅

Perfect understanding:

* Restart service
* Scale resources
* Rollback deployment
* Disable feature flag
* Failover to standby

> Goal = **restore service fast**, not be perfect

---

#### d) Communicate status ✅

Say this clearly in interviews:

* Update status page / Slack / incident channel
* Communicate:

  * What’s impacted
  * ETA
  * Workaround (if any)

---

#### e) Document / Postmortem ✅

Correct.

---

## 2️⃣ Incident Response — refined

Your flow is **right**, just tightening terminology.

### DT-MRP (good structure)

#### 1. Detect

✔ Alerts fired (metrics, logs, health checks)

---

#### 2. Triage ❗ (important concept)

**Triage means:**

* Is this alert real or noise?
* How bad is it?
* Who is affected?

You evaluate:

* Blast radius (1 service vs whole platform)
* Users affected
* Revenue / security impact

👉 Example:

* Disk 80% → warning
* Disk 100% + service down → critical

---

#### 3. Mitigate

Same as on-call → **fast recovery**

✔ Correct

---

#### 4. Resolve

✔ Correct

* Permanent fix
* Code change / infra fix
* Patch, config change, capacity increase

---

#### 5. Postmortem Analysis ✅

Perfect understanding.

Key parts of a **good postmortem**:

* Timeline
* Root cause
* What worked
* What failed
* Action items (alerts, automation)

---

## 3️⃣ Priority handling — your answer is GOOD (minor refinement)

Your answer was solid.
Here is **interview-perfect wording**:

**Priority order**

1. Restore service (mitigation)
2. Reduce blast radius (isolate, rate-limit, disable features)
3. Communicate clearly
4. Identify root cause
5. Prevent recurrence

⚠️ **Never block mitigation for investigation**

---

## 4️⃣ What to do when an incident happens (command flow)

Your flow is **correct**. I’ll clean it:

```
1. systemctl status <service>
2. journalctl / logs
3. Check metrics (CPU, memory, disk, latency)
4. Quick fix (restart / rollback / scale)
5. Validate recovery
6. Add missing alerts / limits
7. Document incident
```

✔ This is **exactly what juniors are expected to do**

---

## 5️⃣ Prometheus / Grafana / PagerDuty / OpsGenie — clarified

### Prometheus

✔ Correct

* Pull-based metrics
* Time-series database
* Uses exporters (node_exporter, app metrics)

---

### Grafana

✔ Correct

* Visualization
* Dashboards
* Can trigger alerts

---

### PagerDuty / OpsGenie

✔ Correct

* Alert routing & escalation
* On-call schedules
* SMS / call / email

---

### Full workflow (you nailed this):

```
App / Node
   ↓
Prometheus
   ↓
Alertmanager
   ↓
PagerDuty / OpsGenie
   ↓
On-call Engineer
```

✔ This is **interview-grade**

---

## 6️⃣ Metrics-Driven Ops — correct

Your statement is very good:

> **No guessing. Decisions based on metrics.**

Add this line:

> Alerts must be **actionable and sustained**, not based on spikes.

Example:

* CPU 90% for 2 seconds → ignore
* CPU 90% for 10 minutes → alert

---

## 7️⃣ SLI / SLO / SLA — mostly perfect

### Small corrections

#### Throughput = ❓ (you asked)

**Throughput means**

* Requests per second
* Jobs per minute
* Messages per second

Example:

* API handles **1,000 requests/sec**

---

### Clean definitions (memorize this)

* **SLI** → What we measure (latency, error rate, availability)
* **SLO** → Target (99.9%, <200ms)
* **SLA** → Business contract & penalties

Your pizza example is **excellent** 👍

---

## 8️⃣ Security incidents — attacks you MUST know (basic list)

You don’t need deep expertise, just awareness.

### Infrastructure / Network

* DoS / DDoS
* Port scanning
* Brute-force SSH
* Credential stuffing

### Application

* SQL Injection
* XSS
* CSRF
* Command Injection

### System

* Privilege escalation
* Misconfigured sudo
* Exposed secrets (.env, keys)

### Cloud

* Public S3 bucket
* Open security groups (0.0.0.0/0)
* Compromised access keys

👉 For SRE roles, **DDoS + brute force + misconfigurations** are enough initially.

---

## 9️⃣ Reality check (important)

### Are you lying if you add this to your resume?

**NO**

Because:

* You understand concepts
* You can explain workflows
* You know tools even if not used in prod yet

### What you SHOULD write

* “Familiar with on-call workflows”
* “Understanding of incident response”
* “Hands-on learning with Prometheus/Grafana (lab)”

---

## 10️⃣ Final verdict (honest)

You are now at:

> **Junior–Mid SRE / Linux Admin readiness**

What you still need:

* 1 Prometheus + Grafana lab
* 1 alert + incident simulation
* 1 postmortem doc in GitHub

That’s **2–3 weeks**, not months.

---

### Next step (don’t skip this)

If you want, next I can:

* Give you **1 fake production outage scenario**
* You respond like an on-call engineer
* I’ll correct you until it’s interview-ready

You’re not behind.
You’re **finally aligned**.

