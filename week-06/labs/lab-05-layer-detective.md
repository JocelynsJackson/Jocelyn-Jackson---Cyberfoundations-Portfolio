# Week 6 Lab 05 — Layer Detective

**Student Name:** Jocelyn Jackson

**Date Completed:** 08/25/26

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-05-layer-detective.md`

---

## Overview

**This is a SHORT lab — 20 to 30 minutes — and it needs no VM.** No Cloud Heights session, no simulator, no screenshot. This is a thinking lab: you take the evidence you have already collected in Weeks 5 and 6 and sort it into layers.

This is an **independent** lab.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | This worksheet only — nothing to start, nothing to connect to |
| Prerequisite | Week 5 labs and Week 6 Labs 01–04 |
| Screenshot | None required |

---

## Part A — The Seven-Row Table

Fill in every row. For the last column, name one **real thing you personally saw** in Weeks 5–6 that belongs at that layer.

| # | Layer name | One-line job | Real thing from Weeks 5–6 |
| --- | --- | --- | --- |
| 7 | Application | Provides network services to applications | HTTP, Ping, SSH |
| 6 | Presentation | Translates, encrypts, and compresses data | TLS, SSL |
| 5 | Session | Manage sessions | Secure Shell (SSH)  |
| 4 | Transport | How data is delivered | TCP, UDP |
| 3 | Network | Networking | IP, Routing, Ping |
| 2 | Data Link | Data processing  | MAC, Switch, ARP |
| 1 | Physical | Hardware  | WIFI, Cables, Fibers |

---

## Part B — Case Files

For each case, name the layer where the problem lives, and name the evidence proving the layers **below** it were already working.

### Case File 1 — The Name That Went Nowhere

A hostname lookup fails, but pinging the machine's IP address directly succeeds.

Layer:

```
Application
```

Evidence that the layers below were working:

```
The issue is not with the network because a ping to the IP address is successful. This shows that the lower layers are working because we are able to ping the machine. The issue is stemming from the Application layer because the hostname is not resolving through DNS.
```

### Case File 2 — Permission Denied

`ssh` to a host returns `Permission denied` after a password prompt.

Layer:

```
Session
```

Evidence that the layers below were working:

```
The Session layer is the issue after the password prompt because SSH is unable to authenticate to the VM. The fact that we are able to reach the password prompt shows that the lower layers are working properly.
```

### Case File 3 — The Cable Story

A machine reports no link on its interface and has no address at all.

Layer:

```
Physical
```

Evidence and reasoning:

```
There is no connectivty at all meaning The Physical layer is the issue because the machine has no link on its interface and does not have an IP address. This suggests there is a problem with the physical connection or network interface, such as an unplugged cable or disconnected.
```

### Case File 4 — Ping Works, The Page Does Not

`ping` to a server succeeds, but `curl http://<that server>` returns nothing useful.

Layer:

```
Application
```

Evidence that the layers below were working:

```
The issue is not with the network because a ping to the server is successful. This shows that the lower layers are working because we are able to reach the server. The issue is stemming from the Application layer because the curl http:// through curl is not responding as it should.
```

### Case File 5 — Wrong Neighbourhood

A machine has an address, but its default route points somewhere that cannot forward its traffic.

Layer:

```
Network
```

Evidence and reasoning:

```
The machine has an IP address, so the network interface is configured. The default route points to a location that cannot forward the traffic, which means the routing is not working properly. This points to an issue at the Network layer because routing and IP addresses are handled at the Network layer.
```

---

## Part C — The Silent Gateway Case

In Lab 03 the Azure default gateway did not answer your ping. However, your VM had a valid default route configured, and your local communication with the Grid Beacon — the ping replies, the HTTP banner, and `TRACE ID: CF-NET-0604` — succeeded.

A failed gateway ping is one piece of evidence — not automatically proof of a gateway or network failure. But the evidence you weigh against it has to be the right kind of evidence.

The Grid Beacon at `10.60.6.4` sits on the same local subnet as your VM (`10.60.6.0/26`). Reaching it proves **local-subnet connectivity** — that traffic never crosses the default gateway, so beacon success alone cannot prove the gateway forwarded anything. Your `ip route` output proves a **default route is configured** — your VM knows where it intends to send non-local traffic — but it does not prove the gateway forwarded that traffic. The evidence that demonstrates the **default path is functioning** is successful communication with a destination outside `10.60.6.0/26`, such as the outbound internet access through NAT that you examined in Lab 04.

### Step 1 — Rule on the Case

Is the failed gateway ping enough evidence to declare a network-layer failure? Explain your answer using the other evidence you collected. In your response, distinguish between:

- evidence that proves **local-subnet connectivity**
- evidence that proves a **default route is configured**
- evidence that supports **successful off-subnet connectivity**

```
A failed gateway ping is not enough to declare there is a network layer failure. The successful Grid Beacon ping, HTTP banner, and TRACE ID: CF-NET-0604 show that the VM is communicating on the local subnet. The ip route output shows that the VM has a default route configured for traffic outside the subnet, but it does not show that the gateway forwarded the traffic. The evidence shows successful communication, such as the outbound internet access through NAT. The failed gateway ping alone does not mean the network is failing.
```

### Step 2 — Name the Correct Conclusion

For each of these four results, state what it actually proves: the Grid Beacon at `10.60.6.4` answering, the default route shown by `ip route`, a successful connection to a destination outside your local subnet, and the gateway's failed ping. Then state the rule you would give a junior colleague about the difference between an observation ("the gateway did not answer my ICMP probe") and a diagnosis ("the gateway is broken"):

```
The Grid Beacon at 10.60.6.4 responding shows that the machine can communicate with that specefic destination over the network. The default route shown by command "ip route" shows that the machine has a pathway for traffic going outside its local network. Successfully connecting to a destination outside the local subnet shows that traffic can leave the local network and reach the destination. The failed ping to the gateway only shows that the gateway did not respond to the request. It does not automatically mean the gateway is broken.

I would tell a junior colleague to focus on what the test shows before jumping to conclusions. An observation is what happened during testing, while a diagnosis helps explain what caused it. It’s always better to get more evidence and test again before saying something is broken.
```

---

## Part D — Two Models, One Job

The OSI model has seven layers. The practical TCP/IP model most engineers speak day to day has four or five.

### Step 1 — Map Them

Briefly show how the seven OSI layers collapse into the practical model:

```
Collapse:

Application, Presentation, Session: Application layer

Transport: TCP/IP Transport layer

Network: TCP/IP Internet layer

Data Link, Physical: TCP/IP Network Access layer

```

### Step 2 — When Each Is Useful

Explain when the seven-layer vocabulary helps and when the practical model is the better tool:

```
The seven-layer vocabulary is helpful when understanding the network as a whole. Understanding each layer individually is important for seeing how they work together and for identifying where problems may occur. The practical model is better for understanding how these layers are used in real-world networks.
```

---

## Analysis Questions

**Analysis Question 1.** Explain the Ladder Rule using layer language. What does "test the near thing first" mean when the rungs are layers? *(Minimum 3 sentences.)*

```
The Ladder Rule means testing the nearest thing first. For example, if you are having an issue at the Network layer, you should test the layers closest to it, such as the Data Link or Transport layer, before checking the Application or Presentation layers. This helps hone in on the problem and narrow down the root cause.
```

**Analysis Question 2.** Why is "which layer is this?" a faster question than "what is broken?" when you are under pressure? *(Minimum 3 sentences.)*

```
You can identify the layer faster than figuring out exactly what is broken. Knowing the layer helps narrow down where the problem is and tells us what to check first. This makes troubleshooting faster because you can focus on the impacted area rather than checking everything.
```

**Analysis Question 3.** Pick one case file from Part B and describe the very next command you would run to confirm your ruling, and what result would change your mind. *(Minimum 2 sentences.)*

```
Case File 3 — The Cable Story

If the device is within my proximity, I would first physically check the device to make sure it is plugged in and wired correctly. The next command I would run to test connectivity is ip link to confirm that the network interface is up and has a physical layer.
```

---

## Submission Checklist

- [ ] All seven rows of the OSI table completed with a real Week 5–6 anchor each (Part A)

- [ ] All five case files given a layer and supporting evidence (Part B)

- [ ] Silent gateway case ruled on correctly (Part C)

- [ ] OSI vs. practical TCP/IP model compared (Part D)

- [ ] All three Analysis Questions answered (minimum sentence counts met)

- [ ] No screenshot required for this lab

- [ ] This file is committed to your portfolio repo at `week-06/labs/lab-05-layer-detective.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 05: Layer Detective** in the Lab Portal.
2. Fill in the worksheet fields.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-05-layer-detective.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
