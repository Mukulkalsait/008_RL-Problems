
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
