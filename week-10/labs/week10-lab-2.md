# Week 10 — Lab 2: Prioritize Risks and Recommend Controls

Learner: Jocelyn Jackson
Case: Cloud Heights Family Clinic — Risk & Threat Investigation
Scenario date: Friday 13 March 2026, 09:00 (clinic local time)
Report generated: 2026-09-27T01:04:53.843Z
Study mode: Guided (hints available)

Completion checklist: all required work for Lab 2 is present.

## Risk ratings

| ID | Asset | Likelihood | Why | Impact | Why | Score (L x I) | Classroom band |
| --- | --- | --- | --- | --- | --- | --- | --- |
| SC-01 | Appointment scheduling account | 2 | The clinic has received multiple similar phishing messages, and staff have been deleting them without reporting them to IT. The scheduling account also does not use MFA. | 3 | If the credentials were compromised, an attacker could access the scheduling system, view or change patient appointments, and potentially disrupt clinic operations or expose patient information. | 6 | High (6–9) |
| SC-02 | Patient records application | 2 | The patient records account is shared, and the credentials are left at the front desk, making it easier for an unauthorized person to access the account. | 3 | An unauthorized user could view, change, or delete patient records, potentially exposing sensitive information and disrupting clinic operations. | 6 | High (6–9) |
| SC-03 | Staff laptops | 3 | The laptops have an unpatched vulnerability that could be exploited by an attacker to gain unauthorized access. | 3 | An attacker could gain access to the laptops and potentially access patient records or other sensitive clinic information, disrupting operations and exposing data. | 9 | High (6–9) |
| SC-04 | Public information website | 2 | The website’s security certificate could expire if it is not renewed on time, causing browsers to warn visitors or block access. | 3 | Visitors may be unable to access the clinic’s website, which could prevent them from finding important information or contacting the clinic online. | 6 | High (6–9) |
| SC-05 | Backup archive | 3 | The backup drive is continuously connected to the workstation, recent backup jobs have completed with errors, and there are no other backup copies. | 3 | If the backup becomes unavailable, the clinic could lose access to important files and have difficulty recovering patient information after a ransomware attack, malware infection, or hardware failure. | 9 | High (6–9) |

Bands (1–2 low, 3–4 medium, 6–9 high) are a classroom teaching aid, not a compliance standard.

## Priority risks
- SC-03 — Staff laptops
- SC-05 — Backup archive

**Why these:** I chose the staff laptops and backup archive because both have a high likelihood and high impact. An unpatched laptop could allow unauthorized access to systems or patient information, while the backup risk could prevent the clinic from recovering important data after a ransomware attack, malware infection, or hardware failure.

## Recommended controls
### SC-03
- **Control:** Apply security patches and updates to all staff laptops as soon as they are available.
- **How it helps:** Patching removes known vulnerabilities that attackers could exploit to gain unauthorized access to the laptops or patient records.
- **Risk remaining afterwards:** The risk is reduced because known vulnerabilities are addressed, but new vulnerabilities or other attack methods could still affect the laptops.

### SC-05
- **Control:** Create a second backup and store it separately from the workstation, such as an offline or cloud backup, and regularly test that backups can be restored.
- **How it helps:** A separate backup provides another copy if the connected backup drive is damaged, encrypted, or unavailable. Restore testing helps confirm that the backup can actually be recovered.
- **Risk remaining afterwards:** The risk is reduced because the clinic has additional recovery options, but backups could still fail or become unavailable if they are not maintained and tested regularly.

## Owner briefing
Word count: 123 (guide: 100–150)

The clinic has several security risks that should be addressed, with the highest priorities being the staff laptops and backup system. Some staff laptops have unpatched security vulnerabilities that could allow unauthorized access to clinic systems or patient information. The clinic should keep all laptops updated with security patches.

The backup system also needs attention. The only backup drive is connected to the reception workstation, recent backups have completed with errors, and there is no second or offsite copy. The clinic should create an additional backup stored separately and regularly test that the data can be restored.

These steps will reduce the chance of losing access to important systems and patient information and improve the clinic’s ability to recover from a security incident.
