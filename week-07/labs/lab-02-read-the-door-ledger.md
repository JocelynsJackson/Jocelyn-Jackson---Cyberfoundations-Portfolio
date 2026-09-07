# Week 7 Lab 02 — Read the Door Ledger

**Student Name:** Jocelyn Jackson

**Date Completed:** 09/06/26

**Module:** 2 — Networking & Cloud Foundations | **Week:** 7  
**Submission Path:** `week-07/labs/lab-02-read-the-door-ledger.md`

> ## Cloud Heights Protected-Rules Safety Rule
> Four baseline rules are protected: **100** (`allow-ssh-from-bastion`), **110** (`allow-icmp-intra-vnet`), **120** (`deny-ssh-student-subnet`), and **1000** (`deny-tcp8080-student-subnet` — Inbound Deny TCP from `10.60.6.0/26` to port `8080`). **You never modify, delete, replace, or use a protected rule as a troubleshooting target.** Create or edit student rules only in priorities **200–999**. The priority **1000** fallback deny sits after your band on purpose, so a narrower Allow you create in 200–999 is evaluated first. A mistake in your student range is recoverable and is not a grading penalty when you diagnose it honestly.

> **Evidence safety:** Never include a Cloud Heights password or Bastion shareable URL. Crop browser address bars and login information before committing screenshots.

---

## Mission

Learn to read inbound and outbound rule ledgers in evaluation order. Translate a rule from field values into plain English, then predict which matching rule makes the decision.

## What You Already Know

A network security rule is a decision about traffic. Rules are evaluated from the lowest priority number to the highest, and the first matching rule wins. Inbound and outbound traffic use separate ledgers. A configured service, a security rule, a test result, and an evidence screenshot answer different questions.

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Cloud Heights → Security Rules |
| Change level | Read-only reasoning |
| Evaluation | Lower priority number first; first match wins |
| Time | 25–30 minutes |

- [x] I am using my assigned `cf-student-XX` VM through the CyberFoundations Lab Portal.

- [x] The VM shows **Running**.

- [x] I can identify the four protected baseline rules at priorities 100, 110, 120, and 1000.

- [x] I understand that my editable priority range is 200–999.

### Cloud Heights Idle Stop

Cloud Heights may warn you that the VM is idle. Return to the Lab Portal and choose **I'm still working** if you are active. If the VM is stopped or deallocated, it was not deleted: restart it from **My Lab Environment**. Your disk files and saved configuration remain.

## Predict First

The priorities **250**, **300**, and **350** used in this lab are **hypothetical examples on paper only — do not create them**. This lab is prediction-only: do not add, edit, or delete rules, and do not run **Test My Rule** unless your instructor tells you to.

Remember the live baseline also contains the protected priority **1000** `deny-tcp8080-student-subnet` fallback (Inbound Deny TCP from `10.60.6.0/26` to port 8080), which is reached only when no earlier rule matches.

Two inbound rules match TCP 8080 from the same source: priority 250 is **Deny** and priority 300 is **Allow**. Predict the verdict before reading further.

```text
Verdict: Denied
The traffic is denied because network rules are checked from the lowest priority number to the highest. Priority 250 is checked before priority 300, and since the priority 250 rule denies TCP traffic on port 8080, it blocks the connection. The priority 300 Allow rule is not reached.
```

## Guided Steps

### Step 1 — Separate the Ledgers

Scroll below the yellow protected-rules summary to the detailed lists headed **INBOUND — EVALUATION ORDER** and **OUTBOUND — EVALUATION ORDER**. Read the inbound list, then the outbound list. Record one sentence explaining why an inbound allow does not automatically create an outbound allow.

```text
Inbound rules control traffic coming in, and outbound traffic leaving the network is controlled by separate rules.
```

### Step 2 — Translate a Rule

Choose one visible protected rule and translate it using this form:

> Read in the [direction] ledger at priority [number], [allow/deny] [protocol] traffic from [source]:[source port] to [destination]:[destination port].

```text
Read in the inbound ledger at priority 100, allow TCP traffic from 192.168.10.128/26:any port to any destination: port 22.
```

### Step 3 — Evaluate in Order

For each hypothetical scenario below, list the rules in evaluation order, identify the first matching rule, and state the verdict. These rules are imaginary — do not create them.

1. Priority 250 Deny TCP from `10.60.6.4` to port 8080; priority 300 Allow the same traffic.
2. Priority 300 Allow TCP from `10.60.6.4` to port 8080; priority 350 Deny TCP from any source to port 8080.
3. An inbound Allow exists, but the traffic being evaluated is outbound.

```text
1. Evaluation order: 250 deny - 300 allow
First matching rule: Priority 250 deny
Verdict: Denied— The lower priority number is checked first, so the deny rule blocks the traffic before the allow rule is reached.

2. Evaluation order: 300 allow - 350 deny
First matching rule: Priority 300 allow
Verdict: Allowed — The allow rule matches first, so the traffic is allowed before the 350 deny rule is checked.

3. Evaluation order: The inbound allow rule does not apply to outbound traffic.
First matching rule: A matching outbound rule must be evaluated.
Verdict: The inbound allow rule does not automatically allow the traffic because separate rules control inbound and outbound traffic.
```

## Stop & Check

If you find yourself reading the Allow you want and ignoring an earlier matching Deny, restart at the lowest priority number. The ledger stops at the first match.

## Test

Use the displayed rule list to predict whether Grid Beacon TCP 8080 would currently be explicitly allowed by a student rule. Do not press **Test My Rule** yet unless your instructor directs you; the service may not be listening.

## Capture Evidence

Capture the detailed **INBOUND — EVALUATION ORDER** view (and **OUTBOUND — EVALUATION ORDER** if your evidence needs it), then name the first matching hypothetical rule and the resulting verdict for each scenario in your worksheet.

![Rule view in evaluation order — week07-lab02-evaluation-order.png](https://raw.githubusercontent.com/JocelynsJackson/Jocelyn-Jackson---Cyberfoundations-Portfolio/refs/heads/main/assets/screenshots/week-07/lab02-evaluation-order.png)

## Explain

Write a five-sentence explanation of first-match-wins that a classmate could use without memorizing Azure terminology.

```text
Rules are checked in order, starting with the lowest priority number and moving to the highest. The system checks each rule one at a time to see if it matches the traffic. Once it finds a matching rule, it follows that rule and stops checking the others. This means a Deny rule with a lower priority number can block traffic before a higher-priority allow rule is reached. If the traffic does not match any rule, it is denied by default.
```

## Required Evidence

Save screenshots in `assets/screenshots/week-07/`:

- `week07-lab02-evaluation-order.png`

Open each image at full size before submission. Confirm that no password, Bastion shareable URL, browser address bar, or unrelated private information is visible.

## Analysis Questions

**Analysis Question 1.** If a Deny at priority 300 and an Allow at priority 400 both match, which wins and why? (Minimum 3 sentences.)

```text
The deny at priority 300 wins because rules are checked from the lowest priority number to the highest. Since 300 is checked before 400 and both rules match the traffic, the Deny rule makes the final decision. The allow rule at 400 is not reached.
```

**Analysis Question 2.** Why do inbound and outbound rules have to be reasoned about separately? (Minimum 3 sentences.)

```text
Inbound and outbound rules have to be reasoned separately because they control traffic moving in different directions. Inbound rules control traffic coming into the network, while outbound rules control traffic leaving the network. An inbound allow rule does not automatically allow outbound traffic because each direction has its own set of rules.
```

**Analysis Question 3.** How can an Allow rule be correct by itself but ineffective in the full ledger? (Minimum 3 sentences.)

```text
An allow rule configured correctly won't work if a rule with a lower priority number matches the rule first. Rules are processed by priority, so the first match always makes the final decision. A lower numbered deny rule can block traffic before an allow rule is evaluated.
```

## Submission Checklist

- [x] Three scenarios evaluated in order

- [x] One live rule translated to plain English

- [x] Inbound and outbound ledgers distinguished

- [x] `week07-lab02-evaluation-order.png` captured

- [x] Protected priorities 100, 110, 120, and 1000 were not changed.

- [x] Every rule I created or edited used priority 200–999.

- [x] No password, Bastion URL, or browser address bar appears in my files.

- [x] This worksheet is committed to `week-07/labs/lab-02-read-the-door-ledger.md`.

## GitHub / Lab Portal Submission

1. Open **Week 7 → Lab 02: Read the Door Ledger** in the CyberFoundations Lab Portal.
2. Complete every worksheet field and confirm the listed evidence filenames.
3. Upload screenshots to `assets/screenshots/week-07/`.
4. Confirm your portfolio repository is connected, then choose **Submit to GitHub**.
5. Open the committed worksheet and each image on GitHub to verify formatting, legibility, and redaction.

*CyberVisionaries Institute · CyberFoundations · Tier I*
