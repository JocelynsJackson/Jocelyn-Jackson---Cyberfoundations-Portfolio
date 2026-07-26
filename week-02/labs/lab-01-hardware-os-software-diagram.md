# Week 2 Lab 01 — Cybersecurity Landscape & Digital Infrastructure Overview

**Student Name:** Jocelyn Jackson

**Date Completed:** 07/26/26

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 2  
**Submission Path:** `week-02/labs/lab-01-hardware-os-software-diagram.md`

---

## Overview

In this lab, you build a working mental model of the system you'll be securing throughout this course: the hardware, operating system, and software layers that make up every computer, and where the cybersecurity field fits around them. This lab has two parts. Part A connects this week's material to the CyberFoundations City map. Part B has you build and explain a diagram of how a computer's hardware, OS, and software layers interact.

**No terminal or command line is required this week** — that starts in Week 3.

---

## Lab Environment

| Component | Details |
|---|---|
| Environment | Browser-based Lab Portal (Module 1 orientation) |
| Required Materials | CyberFoundations City map; a diagram tool of your choice (hand-drawn and photographed, or any digital tool) |

**Prerequisite:** Portfolio repo created from the CyberFoundations student template in Week 1. Fill out this worksheet here in the Lab Portal, then hit Submit to commit it directly to your repo at `week-02/labs/lab-01-hardware-os-software-diagram.md`.

---

## Part A — CyberFoundations City & the Cybersecurity Landscape

The CyberFoundations City map is your visual guide to the next 11 weeks. Each district represents a module of this course. This part connects this week's material to the map you were introduced to in Week 1.

### Step 1 — Open the Lab Portal Orientation Module

From your Student Dashboard, open the **Module 1 orientation** module.

### Step 2 — Complete the Orientation Walkthrough

Work through the orientation content. It covers the same hardware/OS/software material as this week's lessons from a different angle — use it to check your understanding, not to replace the lessons.

### Step 3 — Locate This Week's District on the City Map

Open the CyberFoundations City map (introduced in Week 1, Lesson 6). Identify which district corresponds to Module 1 — Digital Infrastructure & CLI.

**District name:** Foundry District

```
Foundry District consists of the following:
- The Cybersecurity Landscape
- What's Inside a Computer
- Operating Systems at a Glance
```

**Why this district fits this week's topics (1–2 sentences):** Foundry District

```
Foundry is fitting for this week's topic because we are learning the foundation of cybersecurity and its landscape, including the attack surface, defenders, infrastructure, and everyday users' interactions. Foundry is also fitting for learning the fundamentals of computer hardware and its core components and their ins and outs, as well as the basics of OS such as Windows, Linux, and macOS.
```

---

## Part B — Hardware, OS, and Software Diagram

A computer is a stack of layers: physical hardware at the bottom, an operating system managing that hardware in the middle, and the software you actually use on top. This part has you draw that stack and explain it in your own words.

### Step 1 — Identify the Layers

Before drawing anything, name one example of what lives at each layer.

**Hardware layer — one example component (e.g., CPU, RAM, or storage):** CPU (Central Processing Unit)

```
The first layer of a device is the hardware which includes the CPU (Central Processing Unit)is the processor of the computer also considered the "brain" of the computer instructing other parts of the computer what to do.
```

**Operating system layer — name an OS (e.g., Windows, Linux, or macOS):** Linux

```
The second layer of a device includes the OS (Operating System). Linux is an open-source, free, highly customizable operating system commonly used by developers and servers.
```

**Software layer — one example application (e.g., a web browser or word processor):** Web Browser

```
The third layer is the computer's software. While there are many applications, one we use daily while on our phone or computer is the web browser that allows us to connect to the internet
Web browser examples:
- Apple Safari - Available on macOS and iOS devices 
- Google Chrome and Microsoft Edge - Available on many devices and operating systems, including Windows, macOS, iOS, and Android.

```

### Step 2 — Sketch Your Diagram

Sketch a simple diagram (hand-drawn and photographed, or built in any digital tool) showing how the hardware, OS, and software layers stack and interact. Arrows or labels showing "what talks to what" matter more than visual polish. If you'd like a free browser-based option instead of hand-drawing, try [draw.io](https://www.drawio.com/) — no account required to get started.

### Step 3 — Upload and Embed Your Diagram

This step happens directly on GitHub, not through this worksheet — there's no upload field here, since screenshots and diagrams are added through GitHub's own upload UI, the same way as every other week.

1. Go to your portfolio repository on GitHub.com and navigate to `assets/screenshots/week-02/`.
2. Click **Add file → Upload files**, then drag in your diagram image (name it something descriptive, like `hardware-os-software-diagram.png` — no spaces, lowercase, no timestamps).
3. Commit the upload.
4. Click on the uploaded image to open it, then click the **Raw** button. Copy the URL from your browser's address bar.
5. After you submit this worksheet, it will be committed to your repo. Go back to GitHub, open the committed file, click the pencil (edit) icon, and paste your raw URL into the embed line below:

```markdown
![Hardware/OS/software diagram](paste your raw image URL here)
```

**My Diagram** (added directly on GitHub after you submit):

### Step 4 — Explain Your Diagram

In your own words — not a copied definition — explain how the three layers interact. Reference your own diagram directly.

**Explanation (minimum 3 sentences):** Hardware, Operating System and, Software

```
Hardware consists of the physical components of a device such as the motherboard, CPU, RAM, and storage. The operating system is a bridge that manages the device's hardware and allows hardware and software applications to communicate. Software applications are what we use to perform our daily tasks, such as a web browser, a photo editing app, or Word.
```

---

## Analysis Questions

Answer each question in your own words. These questions connect what you did in Parts A and B to the bigger picture of this course.

### Analysis Question 1

If the operating system crashed on the computer you diagrammed, which layer(s) would stop working, and which (if any) would keep working? Explain your reasoning.

```
If the operating system crashed, the OS and software layer would no longer be working, while the hardware would continue to work. The hardware itself will remain functionally running and able to power on and off, but  the features of the device would stop running due to the OS crashing. The hardware cannot connect to the provided resources, and since the OS is down, the software is unreachable.
```

### Analysis Question 2

Pick one piece of software you use daily. Trace it down through the OS to the hardware it ultimately depends on. What would happen to that software if the hardware layer failed?

```
One piece of software I use daily is a web browser Safari on my iPhone and Google Chrome on my Windows desktop. If the hardware layer were to fail, these devices would become inoperable. While the operating system may still technically work, it would no longer be accessible because the hardware has failed. Once the hardware layer fails, we can no longer access the operating system or the software. Software can fail while the operating system continues to function, but if the operating system fails, the software will also be impacted.
```

### Analysis Question 3

Explain, in your own words, why a cybersecurity professional needs to understand all three layers — hardware, OS, and software — rather than just the software layer where most visible attacks (like phishing emails) happen.

```
It is important to understand all three layers of the hardware, OS, and software because these are all attack surfaces. Most visible attacks are coming from the software layer. All aspects of the layer must be protected since they are all connected. If one layer is compromised, it can impact other layers. For example, if the hardware is compromised, the OS can be impacted, affecting the software. This also applies to malicious software being installed on a device, this malicious software can also compromise the OS as well as the hardware.
```

---

## Lab Report Questions

Answer each question in complete sentences.

**1. What is the cybersecurity landscape, and why does it matter to someone starting this course?**

```
The cybersecurity landscape is important to someone starting this course because it shows the bigger picture and the many moving parts of cybersecurity and the constant change. This gives perspective on all the aspects where cybersecurity is needed and how it's used. Attackers, defenders, infrastructure, everyday user. Cybersecurity is a city, not a castle. There are many entry points, attack surfaces, threat landscapes, and digital infrastructure.
```

**2. Which CyberFoundations City district did you identify in Part A, and how does its theme connect to the hardware/OS/software material in Part B?**

```
In the Foundry District, we learned the fundamentals of attack surfaces, threat landscapes, and digital infrastructure and explored the cybersecurity landscape. In Part B we learned how hardware, operating systems, and software interact behind the scenes from end user to device, understanding how these layers work together better helps understand how to better secure a system from attackers.
```

**3. Of the three layers (hardware, OS, software), which one do you think is hardest to secure, and why?**

```
I believe that software is the hardest layer to secure because it is more susceptible to threats and vulnerabilities due to the large attack surface, with constant changes in features, updates, and code changes, which give attackers more opportunities to exploit vulnerabilities.
```

---

## Submission Checklist

- [x] Lab Portal Module 1 orientation completed

- [x] District identified and explained

- [x] Hardware, OS, and software layer examples listed

- [x] Diagram uploaded to `assets/screenshots/week-02/` via GitHub and embedded directly in the committed file

- [x] Diagram explanation written in your own words (minimum 3 sentences)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] All three Lab Report Questions answered in complete sentences

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
