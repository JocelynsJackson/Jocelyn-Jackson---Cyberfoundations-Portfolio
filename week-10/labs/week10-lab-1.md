# Week 10 — Lab 1: Investigate What Needs Protection

Learner: Jocelyn Jackson
Case: Cloud Heights Family Clinic — Risk & Threat Investigation
Scenario date: Friday 13 March 2026, 09:00 (clinic local time)
Report generated: 2026-09-26T23:32:33.258Z
Study mode: Guided (hints available)

Completion checklist: all required work for Lab 1 is present.

## Evidence added to my findings
- EV-REC-02 — Sender address comparison card
- EV-REC-03 — Reception desk log note
- EV-REC-01 — Email received at the reception mailbox
- EV-REC-OFF-01 — Records application account list
- EV-REC-OFF-02 — Records access log extract
- EV-REC-OFF-03 — Practice manager statement — leavers
- EV-WKS-01 — Update status report (IT contractor, 13 March 2026)
- EV-WKS-02 — IT contractor statement
- EV-WKS-03 — Desk photo — signed-in laptop
- EV-WEB-01 — Website certificate details (captured 13 March 2026)
- EV-WEB-02 — Renewal process note
- EV-WEB-03 — What the public website actually holds
- EV-BAK-01 — Backup job history
- EV-BAK-02 — Restore testing statement
- EV-BAK-03 — Backup drive photo

## My investigation notebook
Reception:
On top of the key findings above, a few other suspicious findings are listed below.

Subject line: Urgency in emails with a 2-hour time frame
Requesting a user to confirm a username and password and click on a link is suspicious
Targeting a receptionist who handles patients' sensitive information

Record office:
A card with a password kept at the front desk is a big security issue as is a shared password and account, which makes it hard to track who is responsible for what actions. Even though badges are turned in, a disgruntled ex-employee could still find a way in by piggybacking.

## Risk scenarios

| ID | Asset | Evidence | Threat / event | Vulnerability | Consequence | CIA | Unknown / question |
| --- | --- | --- | --- | --- | --- | --- | --- |
| SC-01 | Appointment scheduling account | EV\-REC\-01 \(Email received at the reception mailbox\) | The receptionist could click the phishing link, potentially downloading malware, and enter their username and password. | The scheduling account uses only a username and password and doesn't implement MFA. The email also uses urgent language, asking the recipient to provide their current password within 2 hours. | The attacker could gain access to the scheduling system, allowing them to view, change, or cancel patient appointments. This could disrupt clinic operations and potentially expose patient appointment information. | Confidentiality, Integrity, Availability | The evidence does not tell us whether the email was responded to, the link was clicked, or if credentials were entered. |
| SC-02 | Patient records application | EV\-REC\-OFF\-01 \(Records application account list\); EV\-REC\-OFF\-02 \(Records access log extract\); EV\-REC\-OFF\-03 \(Practice manager statement — leavers\) | An unauthorized person could use the shared front desk account with credentials left at the desk to access patient records. Because the account is shared, the team would not be able to identify who made any changes.<br> | All four reception staff use the same shared login, and the login remains the same even when someone leaves the company. The password is also written on a card in the desk drawer that could be seen or taken by an unauthorized user, making it difficult to control who can access the account.<br> | An unauthorized user could view patient information, make unauthorized changes, or delete patient records. Because the account and password are shared, and the password is written on a card in the desk drawer that hasn't been changed in 8 months, the clinic may be unable to determine who accessed or altered the records.<br> | Confidentiality, Integrity, Availability | It is unknown whether previous employees can still access the patient records using the shared front desk login. |
| SC-03 | Staff laptops | EV\-WKS\-01 \(Update status report \(IT contractor, 13 March 2026\)\); EV\-WKS\-02 \(IT contractor statement\); EV\-WKS\-03 \(Desk photo — signed\-in laptop\) | An attacker could exploit an unpatched vulnerability on one of the laptops to gain unauthorized access to the device or records application. | The two laptops have not received security updates for 90 days. The updates are still pending because the laptops are used daily, and staff keep postponing the required restart. | If a laptop is compromised, an attacker could gain access to patient records or other clinic information, potentially exposing or altering sensitive data and interrupting normal clinic operations. | Confidentiality, Integrity, Availability | The evidence does not show whether either laptop has actually been compromised or whether the missing updates have caused a vulnerability that can be exploited. |
| SC-04 | Public information website | EV\-WEB\-01 \(Website certificate details \(captured 13 March 2026\)\); EV\-WEB\-02 \(Renewal process note\); EV\-WEB\-03 \(What the public website actually holds\) | Visitors could be prevented from accessing the clinic's website if the security certificate expires and their browsers block or warn them about the site. | The website certificate is renewed manually, with no calendar reminder or named owner responsible for the renewal. Previous renewals were only completed after the site started warning visitors. | Visitors may receive security warnings or have difficulty accessing the website, which could prevent them from viewing important information such as clinic hours, services, and registration instructions. | Availability | It is unknown whether the certificate will be renewed before it expires in 7 days. |
| SC-05 | Backup archive | EV\-BAK\-03 \(Backup drive photo\); EV\-BAK\-02 \(Restore testing statement\); EV\-BAK\-01 \(Backup job history\) | A ransomware attack, malware infection, or hardware failure could make the files and backup data inaccessible.<br> | The only backup is an external drive that remains continuously connected to the reception workstation and was last backed up 14days ago. There are no additional offsite or cloud backups. | The clinic could lose access to patient records and other important files, causing disruption to clinic operations and making data recovery difficult. If damaged or compromised, there are no other copies. | Availability | It is unknown whether the backup data can actually be restored because no restore test has ever been performed. |

## Email analysis
1. From: Clinic IT Support <appointments@clinic-support.example> not support@appointments-vendor.example
2. Urgency in the subject line and a 2-hour time frame
3. Requesting credentials

**Safe response / reporting step:** An appropriate response is not to click the link or provide any credentials. Report the email to the clinic’s IT/security team so they can investigate further and block the sender’s email address from future phishing attempts. The account issue should also be verified directly with the scheduling vendor using the known contact.

**Suspicious vs proven:** The message is suspicious because the sender’s email address does not match the clinic’s legitimate scheduling vendor, and it creates urgency while asking the user to click a link and provide login credentials. The email alone does not prove that anyone entered or used a password. I would need to check the email logs, link destination, and account activity to determine whether anyone interacted with the message or whether the account was compromised.
