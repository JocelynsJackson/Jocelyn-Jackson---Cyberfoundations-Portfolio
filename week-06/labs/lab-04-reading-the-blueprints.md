# Week 6 Lab 04 — Reading the Blueprints

**Student Name:** Jocelyn Jackson

**Date Completed:** 08/24/26

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-04-reading-the-blueprints.md`

---

> ### 🔒 Cloud Heights Security Rule
> Your Bastion link and Cloud Heights password are **private access credentials**. Never paste either into a worksheet, screenshot, GitHub repository, Circle post, or chat message. When taking screenshots, crop out the browser address bar and all login information.

---

## Overview

**This is a SHORT lab — 15 to 20 minutes.** It is deliberately small. You already have the commands; this lab is about matching a drawing to reality.

The **Cloud Heights Network Blueprint** is displayed at the top of this lab page in the portal. Everything you write about the network's architecture comes from that blueprint or from your own machine — never from a guess.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Cloud Heights — live Ubuntu 22.04 VM, reached through Azure Bastion |
| Source of truth | The Cloud Heights Network Blueprint shown at the top of this lab page |
| Commands used | `ip addr`, `ip route` |
| Known value | Student subnet: **`10.60.6.0/26`** |

---

## Part A — Read the Drawing

### Step 1 — Record the Architecture Values

From the blueprint at the top of this page, record each value **exactly as drawn**. If a value is not shown on the blueprint, write "not shown on blueprint" — do not guess.

| Item | Value from the blueprint |
| --- | --- |
| VNet name | vnet-cf-labs |
| VNet address space | 10.60.6.0/24 |
| Student subnet range | 10.60.6.0/26 |

---

## Part B — Verify Against Your Own Machine

### Step 1 — Confirm Your Address Lives in the Subnet

Run `ip addr` and find your private IPv4 address.

Command and output:

```
Command: analyst@cf-student-13:~$ ip addr

Output:
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 60:45:bd:4b:60:d7 brd ff:ff:ff:ff:ff:ff
    inet 10.60.6.32/26 metric 100 brd 10.60.6.63 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::6245:bdff:fe4b:60d7/64 scope link 
       valid_lft forever preferred_lft forever
3: enP51749s1: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc mq master eth0 state UP group default qlen 1000
    link/ether 60:45:bd:4b:60:d7 brd ff:ff:ff:ff:ff:ff
    altname enP51749p0s2
```

Your private IP:

```
10.60.6.32
```

Explain how you know your address falls inside `10.60.6.0/26` — what range does that prefix actually cover:

```
I know my address falls within 10.60.6.0/26 because that is the student subnet range. The 10.60.6.0/26 subnet covers addresses from 10.60.6.0 to 10.60.6.63, and my IP address, 10.60.6.32, is within that range.
```

### Step 2 — Confirm Route Behaviour

Run `ip route`.

Command and output:

```
Command: analyst@cf-student-13:~$ ip route
Output:
default via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.32 metric 100 
10.60.6.0/26 dev eth0 proto kernel scope link src 10.60.6.32 metric 100 
10.60.6.1 dev eth0 proto dhcp scope link src 10.60.6.32 metric 100 
168.63.129.16 via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.32 metric 100 
169.254.169.254 via 10.60.6.1 dev eth0 proto dhcp src 10.60.6.32 metric 100 

O
```

What the default route tells you about traffic that is not destined for your own subnet:

```
The default route tells the network that traffic not destined for my neighborhood (subnet) the traffic is then sent to the default gateway at 10.60.6.1, which then forwards the traffic to its correct neighborhood destination.
```

### Step 3 — Capture Your Evidence

**Required filename:** `blueprint-verified.png`

This must be **your own `ip addr` and `ip route` output** — not a re-screenshot of the blueprint. Crop out the address bar and any login information.

![Blueprint verified — my address inside the student subnet](https://raw.githubusercontent.com/JocelynsJackson/Jocelyn-Jackson---Cyberfoundations-Portfolio/refs/heads/main/assets/screenshots/week-06/blueprint-verified.png)

---

## Part C — How Traffic Actually Moves

### Step 1 — No Public IP

Your VM has a private address and **no public IP**. Explain what that means for who can reach it directly from the internet:

```
When a VM has a private address and no public IP, it is hidden from the public and can only be reached directly by those in the same network.
```

### Step 2 — Outbound vs. Inbound

Outbound internet traffic from your VM leaves through address **translation (NAT)**. Inbound access for you arrives through **Azure Bastion**, not through a public address on the VM.

Explain both directions in your own words:

```
Outbound internet traffic from the VM uses Network Address Translation (NAT) to access the internet. Inbound access is handled through Azure Bastion, so the VM does not need a public IP address.
```

### Step 3 — The Guard Post You Do Not Touch Yet

Each student machine sits behind its own **network security group** — a per-student guard post that decides what traffic is allowed in.

**In Week 6 you do not configure it.** Week 7 is when you take control of those rules.

Write one sentence naming what the guard post does and one sentence stating what you are *not* doing with it this week:

```
A network security group acts as a guard that monitors and controls network traffic coming into the device. This week, we did not configure the security parameters for the group. Next week, we will configure the rules.
```

---

## Analysis Questions

**Analysis Question 1.** Why would an organization put every student machine in one small subnet instead of giving each machine a public address? *(Minimum 3 sentences.)*

```
An organization may put every student's machine on one small subnet instead of giving each machine a public IP address for a few reasons. One reason is security, because machines with public IP addresses can be accessible from the internet, increasing their chances of potential attacks. Reducing cost is another reason because the organization does not need to provide a separate public IP address for every machine.
```

**Analysis Question 2.** Segmentation means separating a network into parts that cannot freely reach each other. Give one concrete benefit of segmentation during a security incident. *(Minimum 3 sentences.)*

```
Segmentation is important because it limits an attacker’s access to other parts of the network during a security incident, reducing the risk of the attack spreading and affecting the entire system. It is easier to isolate and recover one segment of a network than to recover from an incident that causes the entire network to go down.
```

**Analysis Question 3.** A diagram and a live machine disagree about an address range. Which do you trust, what do you do next, and why? *(Minimum 2 sentences.)*

```
The live machine should be the source of truth rather than the diagram because it provides the current, real-time details of the system. The diagram could be outdated, misinterpreted, or contain human errors. When the live machine and the diagram disagree, the live machine should be used to verify the discrepancies.
```

---

## Submission Checklist

- [x] VNet name, address space, and subnet range recorded from the blueprint (Part A)

- [x] `ip addr` run and own private IP confirmed inside `10.60.6.0/26` (Part B, Step 1)

- [x] `ip route` run and default route behaviour explained (Part B, Step 2)

- [x] `blueprint-verified.png` captured from your own terminal, cropped, uploaded to `assets/screenshots/week-06/` (Part B, Step 3)

- [x] Private address / NAT / Bastion explained (Part C, Steps 1–2)

- [x] Per-student guard post identified — and explicitly not configured this week (Part C, Step 3)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-04-reading-the-blueprints.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 04: Reading the Blueprints** in the Lab Portal.
2. Fill in the worksheet fields and upload `blueprint-verified.png` to `assets/screenshots/week-06/`.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-04-reading-the-blueprints.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
