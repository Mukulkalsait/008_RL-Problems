------------------------------------------------------------------
# Incidence:
🔥 **INCIDENT #3 — MEMORY LEAK (High-Severity, Real SRE Scenario)**

---

### 🚨 Alert (02:17 AM)

```
Service: user-profile-api
Severity: P1
Alert: Memory usage > 92% for 15 minutes
Pods restarting due to OOMKilled
```

**Context**

* Traffic: normal (no spike)
* Last deploy: **3 hours ago**
* Other services: healthy
* Node memory pressure observed

---

### Your task 👇

Respond **step by step** in this exact order:

1. **Immediate Actions** (on-call response, priorities)
2. **Investigation** (what you check, how you confirm memory leak)
3. **Mitigation** (short-term + safe recovery)
4. **Communication** (what updates you post)
5. **Post-Incident / Prevention**

🧠 Tip: This one separates **DevOps vs SRE thinking**.

Take your time.
Answer as if this is a **real interview + real on-call**.
----------------------------------------------------

# Response:

1. **Immediate Actions**: (on-call response, priorities):
  - Acknoledgement of alert and stop escalation.
  - Create a slack threat/ incident bridge:
    [Incident-no.xxxxxxx]
    ImpactTime: 02:17-dd.mm.yyyy
    Impact: user-profile-api | Memory usage 92%+ for 15m
    Next Update: 10 min.

2. **Investigation** (what you check, how you confirm memory leak):
    - 92% for 15 min => real alert.
    - user-profile-api pods are restarting => 
    ```bash 
    kubectl info pod_name 
    kubectl logs pod_name 

    kubectl info deployment_name 
    kubectl logs deployment_name 

    kubectl info service_name
    kubectl logs service_name
    ```

    > we will get the exact reason of restart of service or memory leak.

3. **Mitigation** (short-term + safe recovery):
    - last deploy 3 hrs ago. 
    so => really high chances of bad push, but it still took 3 hrs to create alert mean something got full over time. 
    
    1. restart the related service. < some service might be full whose metrics we are not checking> 
    the restart most probably solve the problem temperory if the analysis is right but not a fix.
    2. will  check the above pod info and logs again after restarting each related services. and can find the other 
    service which is getting full. 
    3. this will give us a detaild info of where exactly the problem is.
    4. the permenant fix for that is no DevTeams hand so we will -> ROLLBACK if even after restart we see the things are slowly building up.


4. **Communication** (what updates you post)

    [UPDATE: Incident-no.xxxxxxx]
    ImpactTime: 02:17-dd.mm.yyyy
    Impact: user-profile-api | Memory usage 92%+ for 15m
    Cause: Bad push <user-profile-api service leaking memory. or building up some other service which ultimately making user-profile-api build up ram and 
          the OOMKilled triggered.
    Actions: Restarting the related service => fixes the problem for short time only.
            =>  **ROLLBACK => to the git.version.xxxxxxx**
5. **Post-Incident / Prevention**
    1. we will forward the incident report to dev team showign exact reasons of SLO failure.
    2. we clearly dont have the metrics generation/ visualization for the particular parameter, so will try to build it, 
    as it takes up 3 hr time to create impact we will keep the frequency of pull slight larger like pull every minut or 2 min. 
    3. Documentation of the Whole scenario (i don know how, how do we do that?)

> ok i have some questions here:
 1. what are P1 severity? and what are other  may be p2 p3 and whatever? 
 2. OOMKilled=> if i am not wrong its a kubernetes cluster things where we explicitly define if the memory goes above 
    some threshold its killed. 
    but why OOMKilled name? what are other names like this? 


-------------------------------------------------------------
# Response:

1. **Immediate Actions**: (on-call response, priorities):
  - Acknoledgement of alert and stop escalation.
  - Create a slack threat/ incident bridge:
    [Incident-no.xxxxxxx]
    ImpactTime: 02:17-dd.mm.yyyy
    Impact: user-profile-api | Memory usage 92%+ for 15m
    Next Update: 10 min.

2. **Investigation** (what you check, how you confirm memory leak):
    - 92% for 15 min => real alert.
    - user-profile-api pods are restarting => 
    ```bash 
    kubectl info pod_name 
    kubectl logs pod_name 

    kubectl info deployment_name 
    kubectl logs deployment_name 

    kubectl info service_name
    kubectl logs service_name
    ```

    > we will get the exact reason of restart of service or memory leak.

3. **Mitigation** (short-term + safe recovery):
    - last deploy 3 hrs ago. 
    so => really high chances of bad push, but it still took 3 hrs to create alert mean something got full over time. 
    
    1. restart the related service. < some service might be full whose metrics we are not checking> 
    the restart most probably solve the problem temperory if the analysis is right but not a fix.
    2. will  check the above pod info and logs again after restarting each related services. and can find the other 
    service which is getting full. 
    3. this will give us a detaild info of where exactly the problem is.
    4. the permenant fix for that is no DevTeams hand so we will -> ROLLBACK if even after restart we see the things are slowly building up.


4. **Communication** (what updates you post)

    [UPDATE: Incident-no.xxxxxxx]
    ImpactTime: 02:17-dd.mm.yyyy
    Impact: user-profile-api | Memory usage 92%+ for 15m
    Cause: Bad push <user-profile-api service leaking memory. or building up some other service which ultimately making user-profile-api build up ram and 
          the OOMKilled triggered.
    Actions: Restarting the related service => fixes the problem for short time only.
            =>  **ROLLBACK => to the git.version.xxxxxxx**
5. **Post-Incident / Prevention**
    1. we will forward the incident report to dev team showign exact reasons of SLO failure.
    2. we clearly dont have the metrics generation/ visualization for the particular parameter, so will try to build it, 
    as it takes up 3 hr time to create impact we will keep the frequency of pull slight larger like pull every minut or 2 min. 
    3. Documentation of the Whole scenario (i don know how, how do we do that?)

> ok i have some questions here:
 1. what are P1 severity? and what are other  may be p2 p3 and whatever? 
 2. OOMKilled=> if i am not wrong its a kubernetes cluster things where we explicitly define if the memory goes above 
    some threshold its killed. 
    but why OOMKilled name? what are other names like this?

------------------------------------------------------------------

# Evaluation:

This is **good**. You’re thinking like an on-call SRE already. I’ll do three things:

1. **Correct & sharpen your answer (interview-grade)**
2. **Answer your 2 questions (P1/P2 + OOMKilled)**
3. **Show what an SRE would add vs a DevOps-level answer**

---

## 1️⃣ Feedback + Corrections (important)

### ✅ What you did right

* Acknowledged alert and stopped escalation ✔️
* Created incident channel with **updates cadence** ✔️
* Identified **memory leak grows over time** (key insight) ✔️
* Restart = **temporary relief**, rollback = **real mitigation** ✔️
* Postmortem + metrics gap recognition ✔️

This already passes **junior SRE / strong DevOps**.

---

### ⚠️ What to fix / improve

#### ❌ Command issues (interview red flag)

These commands are **not valid**:

```bash
kubectl info pod_name
kubectl logs deployment_name
kubectl info service_name
```

✅ Correct SRE commands:

```bash
kubectl describe pod <pod>
kubectl logs <pod> --previous   # VERY IMPORTANT for OOMKilled
kubectl get pods -o wide
kubectl describe node <node>

kubectl top pod
kubectl top node
```

**Why `--previous`?**
Because the pod already restarted. Memory leak evidence is in the **previous container**.

---

#### ❌ Missing KEY SRE checks

You must check **limits vs usage**:

```bash
kubectl describe pod <pod> | grep -A5 Limits
```

If:

* usage ↑
* limit fixed
  → OOMKilled is **expected behavior**, not infra bug.

---

### ✅ What an SRE would explicitly say

Add **this sentence** in interviews:

> “Restart only reduces symptoms; rollback stops leak propagation.”

That sentence alone signals **SRE maturity**.

---

## 2️⃣ Your Questions Answered (very important)

---

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

## Q2️⃣ What exactly is OOMKilled?

### 🔹 Meaning

**OOM = Out Of Memory**

OOMKilled means:

> **Kernel / container runtime forcibly killed the process to protect the node**

It’s a **Linux kernel behavior**, surfaced by Kubernetes.

---

### 🔹 Why this name?

Linux has an **OOM Killer**:

* When memory exhausted
* Kernel chooses a process
* Kills it to save the system

Kubernetes reports that as:

```
Reason: OOMKilled
Exit Code: 137
```

---

### 🔹 Why Kubernetes kills it

Because you defined:

```yaml
resources:
  limits:
    memory: "512Mi"
```

If app exceeds it → **K8s is doing its job**

---

### 🔹 Other common Pod termination reasons you MUST know

| Reason           | Meaning                   |
| ---------------- | ------------------------- |
| OOMKilled        | Memory limit exceeded     |
| CrashLoopBackOff | App crashes repeatedly    |
| Error            | App exited with non-zero  |
| Evicted          | Node under pressure       |
| ImagePullBackOff | Image not pulled          |
| NodeNotReady     | Node issue                |
| Completed        | Job finished successfully |

If you say **3–4 of these in interview**, you stand out.

---

## 3️⃣ Why this answer is SRE (not just DevOps)

### DevOps would say:

> Restart service, rollback if needed

### SRE says:

* Leak grows over time
* Memory limit behavior understood
* Restart = symptom relief
* Rollback = blast radius reduction
* Metrics gap identified
* Postmortem with prevention

That’s why **SRE > DevOps** in responsibility, not hierarchy.

---

## 🔥 Verdict on you (honest)

* **DevOps: ready**
* **Junior SRE: yes**
* **Mid SRE: not yet (needs hands-on Prometheus + K8s memory debugging)**

You are **not faking knowledge** — you’re building it correctly.

---


