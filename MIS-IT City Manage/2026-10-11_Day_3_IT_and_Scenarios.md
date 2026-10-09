# 11 October 2026 — Day 3: IT, portals and municipal scenarios

Today’s goal: answer practical problems with a clear process and sensible judgement.

## Study order — approximately four hours

- [ ] 30 minutes: explain yesterday’s Excel report as if speaking to an officer.
- [ ] 60 minutes: learn IT concepts and practise the troubleshooting sequence.
- [ ] 45 minutes: revise the reporting workflow and sanitation reminders below.
- [ ] 30 minutes: study basic SQL; treat this as optional if time is short.
- [ ] 60 minutes: practise the 13 scenario answers below.
- [ ] 15 minutes: record your introduction and one scenario answer; listen and improve.

If you have only two hours: 45 minutes IT, 45 minutes scenarios and 30 minutes spoken practice. Skip SQL until the higher-priority topics are comfortable.

## Quick reminders from the first two days

- MIS turns checked records into information for decisions.
- Workflow: collect → validate → reconcile → approve → submit → retain evidence → follow up.
- Check period, ward, units, source evidence and denominator.
- Missing data is not zero; do not invent records to meet a deadline.
- SBM-U 2.0 has a garbage-free-city vision.
- Source segregation means separating waste where it is generated.
- Collection, generation and processing quantities are not automatically interchangeable.
- A geotag or portal status alone is not proof that the full service was completed.

## Basic IT and office skills

### Concepts in plain language

- Hardware is the physical equipment; software is the operating system and applications.
- RAM is working memory; storage keeps saved files. An SSD is storage, not RAM.
- An operating system manages hardware and applications.
- A LAN connects devices within a local area; the internet connects networks more widely.
- An IP address identifies a network interface; DNS helps translate names to IP addresses.
- A switch connects devices in a network; a router forwards traffic between networks.
- HTTP is a web protocol; HTTPS adds encrypted transport using TLS. HTTPS alone does not prove a site is trustworthy.
- A browser opens websites; a search engine helps find them.
- A database stores structured records; a primary key uniquely identifies a row.
- A PDF is useful for fixed-layout sharing; CSV stores plain tabular text and does not preserve workbook formulas, charts or multiple sheets.

### Troubleshooting method

Ask what failed, when it began, what changed, who is affected, and the exact error. Check simple causes first. Try one reversible change at a time within your access level. Record what you tried, escalate with useful evidence if needed, and verify the service works afterwards.

**No internet:** check whether one website or every website fails; whether only one device or the whole office is affected; Wi-Fi/Ethernet connection; another permitted browser/site; network settings and the approved IT support route. Do not reset shared equipment during other staff's work without coordination.

**Printer not printing:** check power, paper, error display and connection; correct printer selection; offline status; stuck jobs; and a test page. If a driver or shared printer service needs attention, use authorised support. Verify with the user after recovery.

**Slow computer:** check free space, unusually busy applications, startup workload and updates; save work before restart; use the approved security scan if appropriate. Avoid downloading unknown “speed booster” software.

**Portal upload fails:** check the authorised URL, network, session, required fields, file type/size, readable evidence and exact error. Save the report and timestamped error evidence. Check whether submission already succeeded before retrying. Escalate before the deadline with the affected report and error details.

**Backup:** use the office's approved backup location and schedule, protected access and periodic restore checks. A successful copy is not proof of a working backup until recovery is checked.

**Phishing:** verify unexpected senders and requests through a known contact route; do not share passwords/OTPs; report suspicious messages. Use official account recovery instead of asking another person for credentials.

### Office tasks to practise once

- Word: write a short letter with date, subject and signature block; export to PDF.
- Email: write a clear subject, brief summary, requested action and attachment reference; check recipients and attachments before sending.
- PDF/scanning: ensure pages are upright, readable and complete; use approved tools to combine or resize documents when needed.
- Presentation: explain one chart with its period, units, main issue and next action.
- Gujarati typing: practise if it is part of your experience; describe your actual ability honestly.

Illustrative email draft for practice only:

> Subject: Review requested — daily sanitation MIS — 09 October 2026
>
> Sir/Madam, please find the practice ward summary attached for review. The source records have been checked, and one missing evidence reference is marked pending. Please advise on the pending item before submission. Regards, [name].

## Basic SQL: optional supporting preparation

SQL queries structured data. Learn SELECT (retrieve), WHERE (filter), ORDER BY (sort), GROUP BY (group totals) and COUNT/SUM (aggregate). WHERE filters rows before aggregation; HAVING filters groups. Primary keys identify records and foreign keys link related records. Source for query clauses: [PostgreSQL SELECT documentation](https://www.postgresql.org/docs/current/sql-select.html); [basic querying tutorial](https://www.postgresql.org/docs/current/tutorial-select.html).

The following are original examples for a hypothetical table `ward_daily` with fields `report_date`, `ward_id`, `waste_kg`, `processed_kg`, `complaints`. They are learning examples, not instructions to access a municipal database.

```sql
-- Retrieve selected columns for one reporting date.
SELECT ward_id, waste_kg, complaints
FROM ward_daily
WHERE report_date = '2026-10-09'
ORDER BY complaints DESC;

-- Sum waste by ward across the available records.
SELECT ward_id, SUM(waste_kg) AS total_waste_kg
FROM ward_daily
GROUP BY ward_id;

-- Find repeated date + ward combinations for review.
SELECT report_date, ward_id, COUNT(*) AS record_count
FROM ward_daily
GROUP BY report_date, ward_id
HAVING COUNT(*) > 1;
```

For the sample: the first query starts with Ward 2, eight complaints; the second gives Ward 1 **1020**, Ward 2 **1380**, Ward 3 **1210 kg**; the third returns no rows if the six practice records are entered once. Repeated keys are a signal to inspect the data, not automatic proof that a row should be deleted.

If asked about JOIN: it combines related tables using matching keys, such as a ward master and daily records. INNER JOIN keeps matches; LEFT JOIN can retain daily records even when the master match is missing. You can explain the concept without claiming database administration experience.

## Today's scenario questions and answers

Use this response pattern: identify the problem → check facts → act within authority → document/escalate → verify the result.

**18. The portal is down near a deadline.** Save the validated report, record the error and time, check scope/connectivity, notify the supervisor and authorised support, and use only an approved alternative if available. Preserve evidence and acknowledgement; do not backdate submission.

**19. Someone asks you to inflate a figure.** Explain that figures need source evidence. Present the actual records and discrepancy, seek clarification through the supervisory route and keep an appropriate record. Do not fabricate data.

**20. A citizen complaint has no clear location.** Politely request the minimum details needed, record the complaint, route it to the responsible staff and track the next action under the prescribed process.

**21. A complaint is marked resolved but the citizen disagrees.** Review closure evidence, coordinate verification, and reopen or escalate according to the system's process. A status field alone is not proof of resolution.

**22. How would you protect municipal data?** Use authorised accounts and storage, appropriate access, protected backups and verified recipients. Do not share credentials or unnecessary citizen information.

**23. What is a backup?** A protected recoverable copy of data. I would follow the approved backup schedule and test restoration, not just check that a copy exists.

**24. The office printer stops working.** Check power, paper, errors, connection, printer selection and queue; try a test print; escalate driver/shared-service issues within the authorised process and confirm recovery.

**25. Staff are late sending records.** Use a simple standard template and clear deadline, identify the reason, send reminders, flag pending records and escalate early. Never invent the missing entries to finish the report.

**26. How will you teach staff a reporting format?** Demonstrate a short example, explain required fields and common errors, let them practise, then provide a brief checklist and follow-up support.

**27. Two urgent tasks arrive together.** Clarify deadlines and impact, agree priorities with the supervisor, divide the work into steps and communicate any risk early. Keep accuracy checks even under time pressure.

**28. How can technology improve cleanliness work?** Consistent ward records and location-linked complaints can help identify repeat gaps and track actions. A simple reliable process should come before proposing new software.

**29. What would you do in your first month?** Learn current reporting requirements, access controls and source records; check missing data and evidence; standardise templates with approval; establish review, submission and follow-up routines; share the main issues with the officer.

**30. You discover an error after submission.** Tell the designated officer promptly, document the error and supported correction, use the approved correction process and retain the revision trail. Investigate why it happened to prevent repetition.

## Spoken practice

1. Explain a printer failure in 60 seconds.
2. Explain a portal failure before a deadline in 90 seconds.
3. Explain a mismatch between field records and uploaded figures.
4. Explain what you would do if asked to inflate a figure.
5. Describe your first month in the job.
6. Give one genuine example of teamwork or troubleshooting.

## End-of-day check

- [ ] I can troubleshoot step by step.
- [ ] I can explain how to handle a failed portal submission.
- [ ] I can explain data protection and recoverable backups.
- [ ] I can explain complaint follow-up and verification.
- [ ] I can answer a difficult scenario without inventing facts.

Scenario I can explain confidently:
One real experience example:
Three weak answers to fix tomorrow:

Next: [12 October — mock interview and final preparation](./2026-10-12_Day_4_Mock_and_Final_Preparation.md).

Preparation material organised from the [complete researched guide](./Interview_Preparation_09_to_13_October_2026.md). Suggested topics and questions are not an official interview syllabus.
