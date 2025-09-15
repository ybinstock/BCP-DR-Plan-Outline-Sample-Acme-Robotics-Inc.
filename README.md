# BCP-DR-Plan-Outline-Sample-Acme-Robotics-Inc.

Table of Contents

Executive Summary

Scope, Assumptions, Roles

System Tiers & RTO/RPO Matrix

Communications Templates

Quarterly Restore Test Plan

Tabletop Exercise Outline

Vendor Dependency List

Recovery Runbooks

Post-Incident Review & Improvements

Metrics & Reporting

Audit-Ready Evidence Checklist

Change Management Linkage

Glossary

Changelog

Executive Summary

Acme Robotics, Inc. has established this Business Continuity and Disaster Recovery (BCP/DR) plan to ensure the company can sustain critical operations and recover IT systems in the event of a disruption. This plan covers preparation, response, and recovery strategies for incidents ranging from data center outages to cybersecurity events.

Key Recovery Objectives: Tier 0 (life/safety) services have a 15-minute Recovery Time Objective (RTO) and near-zero Recovery Point Objective (RPO). Tier 1 (mission-critical) systems target 1 hour RTO and 15 minutes RPO, with lower priority tiers allowing progressively longer RTO/RPO (up to 72 hours RTO for Tier 4).

Note: This document is sample content for demonstration purposes only—all data and scenarios are fictitious.

Scope, Assumptions, Roles

Scope: Covers preparedness, emergency response, IT recovery, and business resumption. Focus is on significant disruptions (e.g., primary data center loss). Minor outages and routine maintenance are out of scope.

Assumptions:

Complete loss of us-west region possible.

Key staff or alternates available.

Off-site backups intact.

Vendors honor SLAs.

At least partial comms networks available.

RACI Roles:

Task	BCP Lead	DR Runbook Owner	Comms Lead	Vendor Manager	Legal/Privacy
Plan Maintenance	A	R	C	C	C
Plan Activation	R	A	I	C	I
Technical Recovery	C	R	I	C	I
Internal Communications	C	I	R	I	C
Customer/Vendor Communications	I	I	A/R	R	C
Regulatory Coordination	I	I	C	C	A/R
System Tiers & RTO/RPO Matrix
Tier	Example Systems	Criticality	RTO	RPO	Recovery Order	Dependencies
0	Emergency Alerting	Highest (safety)	15m	0m	1	SMS Gateway, Redundant ISP
1	AuthX, BillingApp	Very High	1h	15m	2	DB, PKI, DNS
2	IoT API, Customer Portal	High	4h	1h	3	Object Store, MQ
3	Analytics, Data Warehouse	Medium	24h	8h	4	Data Lake
4	Internal Wiki	Low	72h	24h	5	SSO
Communications Templates

Internal Incident Notice

[Timestamp] INTERNAL INCIDENT NOTICE – [System]
Impact: [Teams/Systems]
Status: [Issue description]
Next Update: [Time]
Owner: [On-call manager]
Action underway: [What team is doing]. Updates by [time].

Customer Update (Status Page)

[Timestamp UTC] Service Disruption: [Service]
Impact: [What’s broken]
Current Status: [What’s being done]
Next Update: [Time/ETA]
Questions? support@acmerobotics.example

Recovery Complete Notice

[Timestamp] RECOVERY COMPLETE – [Incident ID]
Summary: [What happened]
Resolution: [How fixed]
Data Integrity: [Data check result]
Owner: [Name, Title]
Contact: incident@acmerobotics.example

Quarterly Restore Test Plan

Objectives: Verify backups, restore speed, runbook accuracy, key access.
Scope: Each quarter, test 2–3 systems from different tiers.
Schedule: Once per quarter during maintenance window.

Test Steps:

Validate backups exist.

Restore to isolated environment.

Validate data integrity and app function.

Capture duration, compare to RTO.

Cleanup/failback.

Success Criteria: RTO/RPO met, data integrity passes, sign-offs obtained.
Artifacts: Logs, screenshots, timings, runbook diffs.

Sample Metrics Table:

Quarter	System	Backup Date	Start	End	Duration	Checksum OK	Owner	Notes
Q1-2025	AuthX	2025-01-02	10:00	10:45	45m	Yes	DevOps	Passed
Q2-2025	PortalApp	2025-04-05	09:00	10:30	90m	No	IT Eng	Re-test req.
Tabletop Exercise Outline

Scenario: us-west outage + IdP vendor down.
Objectives: Decision speed, comms clarity, escalation, prioritization.
Participants: Exec Sponsor, Incident Commander, Ops, Security, Comms, Support, Legal.

Agenda:

0–10m: Kickoff

10–25m: Inject #1 (region outage)

25–45m: Inject #2 (backup access fail)

45–65m: Inject #3 (customer data concern)

65–90m: Inject #4 (vendor SLA breach)

90–110m: Recovery decisions

110–120m: Hotwash

Scoring: Clarity, speed, accuracy, ownership, documentation (1–5 scale).

Vendor Dependency List
Vendor	Service	Tier Impact	SLA	Evidence	Contact	Exit Strategy
CloudCo	Storage	1–3	99.9% / 4h	Attestation 2025	ops@cloudco.example
	Multi-region + weekly export to AltStore
AuthWorks	SSO/IdP	1	99.95% / 1h	SOC2 (fake)	support@authworks.example
	Break-glass accounts + backup config
TextAlertCo	SMS	0	99.5% / 2h	BC Test 2025	noc@textalertco.example
	Backup SMS provider/manual phone tree
PayPartner	Payments	1–2	99.9% / 2h	SOC Reports	support@paypartner.example
	AltPay/manual processing
MailSend	Email	2–3	99% / 24h	None	support@mailsend.example
	BackupMailer or queue messages
DNSCorp	DNS	0–4	99.99% / 30m	Report 2025	dns@dnscorp.example
	AlternateDNS or local hosts files
Recovery Runbooks

Sample: AuthX Authentication (Tier 1)

Preconditions: Primary down, secondary up.

Tools: VPN, Vault creds secret/prod/authx/admin.

Steps: Deploy DR servers, restore DB, update configs, cut DNS, test logins, comms update.

Verification: Users can authenticate; data intact.

Rollback: Revert DNS or use alternate IdP.

Sign-off: BCP Lead + System Owner.

Post-Incident Review & Improvements

Template:

Summary: [Incident details]

Timeline: [Key events/times]

Root Causes: [Underlying issues]

Impact on RTO/RPO: [Met or missed]

What Went Well: [Strengths]

Improvements: [Gaps]

Actions:

[Task] – Owner – Due Date

[Task] – Owner – Due Date

Metrics & Reporting
Metric	Value (Q4 2025)
DR Test Pass Rate	75%
Avg Restore Duration vs RTO	90%
Backup Success Rate	98%
Comms SLA Met	100%
Vendor DR Evidence Freshness	80%
Audit-Ready Evidence Checklist

Current BCP/DR plan and changelog

DR test logs and results

Recovery runbooks with update dates

Backup logs and screenshots

Incident comms archives

Post-incident review reports

Vendor attestations and SLA docs

CAB records showing BCP/DR updates

Change Management Linkage

BCP/DR artifacts are updated through CAB reviews. Major infra or app changes trigger DR runbook reviews. IaC ensures DR configs track production. A quarterly BCP committee review keeps plans accurate.

Glossary

RTO: Max downtime allowed.

RPO: Max data loss allowed.

Tier: Priority classification for systems.

Tabletop: Discussion-based simulation.

Restore Test: Backup recovery drill.

Break-glass: Emergency account with high access.

Hotwash: Immediate post-incident debrief.
