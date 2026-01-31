# 🚨 NEXT INCIDENT 

**INCIDENT #4 — LATENCY + NO ERRORS**

```
P2 Alert:
API latency p95 > 2.5s for 20 min
Error rate: normal
CPU/memory: normal
Traffic: normal
```

👉 This one is **pure SRE thinking**.
 
-----------------------------------------


# Response:

I I M C PP

### 1.Immediate action: 
  1. Acknowledgement of the Alert to stop escalation.
  2. Create Slack thread / Incident Response Bridge:
    [Incident:xxxxxxxxx]
    ImpactTime: MM.HH DD.MM.YYYY
    ImpactArea: Latency SLO fail.
    NextUpdate: 15 Min

### 2.Investigation:
  - Thinking
    1. if all the apis are affected, or specific onc only.
    2. if specific are affected, service related issue if all afected, check may be network related issues.
    (even though i mention bot things i dont know how do i check both of them. please explain me.)
    3. Check last Deployment time.
    4. check logs -> warning and above level. 
    5. use more monitoring like 
      - Network monitoring, connection monetoring, database moniigoring, dependncy usage monitoring, Cache save check and monitoring.

### 3. Mitigation:
  - Rollback is a last option in such cases.
    1. might be Network related issue. 
    2. slower networ, multycloud network issue like some dependncy of storage from other cloud is not configured probpely. 
    3. fuguring out that and reconfiguring it is the most important Things.
    4. this might take time but we dont have options if things did not workout rollback + check matrices if the issue resolved. 
        if rollback is not solving issue then the problem should be solve on SRE side.
    5. checking and reconfiguring services related to the issue, and logs should also be checked.

### 4. Communication:
 - we might not be able to get to root cause fast so. 
    [Update Incident:xxxxxxxxx]
    ImpactTime: MM.HH DD.MM.YYYY
    ImpactArea: Latency SLO fail. + added informationo.
    Cause: < found cause> 
    Actions: Reconfigure services if they are culprit.
    Postmortem: will be published in next update
    NextUpdate: 1-2Hr.

### PostMortem/Prevention:
  - nil.
    i am not geting any idea in this section, may be going through logs will somehow help,
    please guide me here. 

## Questions: 
   1. what are this latency types p95 > 2.5 for 20min?


---------------------------------------------

# Evaluation: 

Perfect. This is exactly how this game should work 👍
I’ll **rate you**, **fix gaps**, **teach missing concepts**, and **upgrade your answer to interview-grade SRE**.

---

# 🔥 INCIDENT #4 — EVALUATION

## ⭐ Overall Rating: **5.8 / 10**

### 📊 Level Assessment

**Early DevOps → Aspiring Junior SRE**

You’re thinking in the **right direction**, but this incident exposes **SRE-specific gaps** (which is normal). This is a *classic SRE interview trap*.

---

## ✅ What You Did RIGHT (important)

These saved you from a low score:

1. ✅ Proper **ack + incident bridge + update cadence**
2. ✅ Asked the **right first question**:

   > “Is it one API or all APIs?”
3. ✅ Understood rollback is **not the first reaction**
4. ✅ Thought about **network, dependencies, DB, cache**
5. ✅ Honest admission of uncertainty (better than guessing)

This shows **real thinking**, not memorization.

---

## ❌ Where You Lost Points (critical gaps)

I’ll be very direct.

### ❌ 1. You didn’t anchor on the KEY signal

This line is the **entire incident**:

```
Latency high
Errors = normal
CPU = normal
Memory = normal
Traffic = normal
```

👉 This immediately means:

> **The system is waiting, not failing**

You didn’t explicitly say that — an SRE **must**.

---

### ❌ 2. Investigation was too abstract

You said *what* to check, but not **how**.

In SRE interviews, this is a red flag unless corrected.

---

### ❌ 3. Mitigation section was weak

You jumped to:

* network issues
* multicloud
* rollback

Without **proof signals first**.

SREs are **evidence-driven**, not assumption-driven.

---

### ❌ 4. Postmortem = nil ❌ (big penalty)

In SRE:

> **If there’s no postmortem, the incident isn’t finished**

This alone dropped you ~1 full point.

---

## 🧠 Now let’s UPGRADE your answer (this is the learning part)

---

# ✅ IDEAL SRE RESPONSE (What interviewers expect)

## 1️⃣ Immediate Actions

(Your part was good — no changes needed)

---

## 2️⃣ Investigation (THIS is where SREs shine)

### 🔑 Core SRE Insight (say this explicitly)

> “High latency with no errors and normal resources means requests are **blocked or waiting** on something external.”

### Step-by-step checks (concrete)

#### 1. Scope the blast radius

```text
- One endpoint or all?
- One AZ(avialabtlity Zone) or all?
- One pod or all replicas?
```

How:

* APM (Grafana / Datadog / NewRelic)
* Per-endpoint latency dashboards

---

#### 2. Check dependency latency (MOST IMPORTANT)

Latency without errors usually means:

* DNS delay
* External API slow
* Cache misses
* Connection pool exhaustion
* Database slow

What to check:

* DB query p95 latency
* Redis hit/miss ratio
* External API response time
* Connection pool usage

---

#### 3. Check saturation signals (not CPU)

SRE golden signals:

* **Latency**
* **Traffic**
* **Errors**
* **Saturation**

Here, saturation might be:

* DB connections maxed
* Thread pool exhausted
* Queue depth increasing

---

#### 4. Check retries & timeouts

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

### What NOT to do immediately

❌ Rollback (no deploy happened)
❌ Restart (will not fix waiting)

---

## 4️⃣ Communication (improved)

Key SRE phrasing:

> “No user-visible errors, but response times are degraded.
> We suspect downstream dependency slowness.”

This reassures stakeholders.

---

## 5️⃣ Post-Incident / Prevention (YOU MUST HAVE THIS)

Examples you could say:

1. Add **per-dependency latency SLOs**
2. Enforce **timeouts + circuit breakers**
3. Alert on **p95 dependency latency**
4. Load test with slow-dependency scenarios
5. Improve dashboards for saturation signals

Even **2 of these** would’ve boosted your score to **7+**.

---

## ❓ Your Question Answered

### Q️⃣ What is `p95 latency > 2.5s for 20 min`?

This is **very important SRE knowledge**.

#### p95 means:

> 95% of requests are faster than this number

So:

```
p95 = 2.5s
```

Means:

* 95% of users waited **up to 2.5 seconds**
* Worst 5% may be even slower

#### Why p95 (not average)?

* Averages hide pain
* Tail latency kills user experience

#### Why “for 20 minutes”?

* Avoid alert flapping
* Ensure sustained degradation, not spike

---

## 📈 Revised Score IF YOU SAID THE IDEAL ANSWER

👉 **8.1 / 10 (Solid Junior SRE)**

You’re **very close**. This incident is genuinely hard.

---

## 🧠 One-line SRE takeaway (memorize this)

> **High latency + no errors + normal CPU = waiting on dependencies**

Say this once in interviews → instant credibility.




