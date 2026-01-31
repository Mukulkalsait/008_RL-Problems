
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
