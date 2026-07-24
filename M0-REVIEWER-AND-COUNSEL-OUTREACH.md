# M0 Exit Criteria: LoC Labs / By the People Outreach + Rights Reviewer and Counsel Appointment

**Status:** In Progress  
**Date Started:** 2026-07-24  
**Last Updated:** 2026-07-24  
**Owner:** TBD (implementer)

---

## Executive Summary

This document records the outreach to the Library of Congress Labs and By the People (Concordia) program, and tracks the identification, vetting, and appointment of:
1. A **qualified rights reviewer** for the rights-vocabulary ruleset (hard M0 exit criterion)
2. **Counsel or qualified rights/IP attorney** to review the rights/vocabulary.yml mapping

This is a required M0 exit criterion (per PLAN.md, Governance section, exit criteria f and g). **M0 cannot exit until these roles are filled.**

---

## Part 1: LoC Labs Outreach

### Research & Contact Information

**Organization:** Library of Congress Labs  
**Mission:** Digital innovation and experimental projects at the Library of Congress  
**Website:** https://labs.loc.gov/  
**GitHub:** https://github.com/LibraryOfCongress/ (primary technical contact channel)

#### Known Contact Pathways
1. **General LoC Contact Form:** loc.gov/contact
2. **LoC Labs GitHub:** Issues/discussions on relevant projects
3. **Technical/API Questions:** Often routed through main LoC Contact Center or specific project repositories

#### Collaboration Relevance
LoC Labs is the appropriate contact for:
- API usage etiquette and best practices guidance
- Bulk data offerings and sitemap availability verification
- Current rate-limiting policies and any planned changes
- Potential collaboration opportunities around public-domain clearing
- Feedback on the polite-access protocol design

### Outreach Status

- **Status:** NOT YET INITIATED  
- **Next Step:** Send introductory email (see template below)
- **Target Response Time:** 2-4 weeks
- **Follow-up:** If no response by [DATE], escalate to general LoC Contact Center

#### Outreach Template: LoC Labs Introduction Email

```
Subject: API Collaboration Inquiry — Public Domain Rights-Gate + Polite Access Protocol

To: [LoC Labs contact, TBD]
From: [Your name/Hee-Lee Oss]

Dear [LoC Labs team / specific contact if identified]:

I am reaching out on behalf of Hee-Lee Oss, a collaborative open-source initiative focused 
on public-good digital projects.

We are developing a **rights-gate and polite API-access protocol** over the Library of 
Congress public-domain item collection. The project (loc-public-domain-engine, in public 
beta at https://github.com/Hee-Lee-Oss-Projects/loc-public-domain-engine) is designed to:

1. **Conservative rights-gating:** Clear only affirmative, recorded public-domain/open-license 
   items from LoC's metadata using an allow-list approach (deny-by-default).
2. **Polite API access:** Honor LoC's published rate-limit policy, use conditional requests 
   + caching to reduce server load, implement backoff + circuit-breaker patterns, and identify 
   the crawler via contact User-Agent.
3. **Reproducible provenance:** Emit frozen manifests (raw API snapshot, rights determination, 
   timestamp, content hash) so every cleared item is auditable.
4. **Downstream fan-out:** Feed cleared items into Hee-Lee Oss projects for transcription, 
   alt-text generation, translation, and structured datasets.

**We are seeking input on:**
- Current LoC per-endpoint rate-limit policies (to populate our `loc-policy.yml`)
- Availability of bulk-data packages, item sitemaps, or collection manifests (to prefer 
  over per-item crawling)
- Best practices for responsible API access at scale
- Any existing LoC initiatives or collaborations with public-domain derivative projects

**We believe this project aligns with LoC's mission** to make public-domain material more 
accessible and discoverable. We are keen to establish an ethical collaboration and would 
welcome any guidance, feedback, or partnership opportunities.

Would you be available for a brief conversation (15-30 minutes) to discuss this? We can 
accommodate any format (email, call, async video) that works best for your team.

Thank you for considering this outreach. I look forward to hearing from you.

Best regards,
[Your name]  
[Your email]  
[Project URL]  
[Phone (optional)]
```

### Outreach Record

**Outreach Attempt #1:**
- **Date Sent:** [TO BE RECORDED]
- **Method:** Email
- **Contact:** [NAME/EMAIL]
- **Response Status:** Awaiting response
- **Response Date:** [TO BE RECORDED]
- **Summary:** [TO BE RECORDED]
- **Engagement Status:** ☐ No response ☐ Received response ☐ In conversation ☐ Collaboration confirmed

**Follow-up Actions:**
- [ ] If no response after 2 weeks, resend with note: "Following up on the inquiry sent on [DATE]."
- [ ] If response received, log details and next steps below.

---

## Part 2: By the People / Concordia Outreach

### Research & Contact Information

**Organization:** "By the People" (Concordia platform)  
**Operated By:** Library of Congress  
**Mission:** Crowdsourced transcription and correction of historical documents and photographs  
**Website:** https://bythepeople.loc.gov/  
**GitHub (if public):** Check https://github.com/LibraryOfCongress/ for Concordia project

#### Known Contact Pathways
1. **Main Contact Form:** bythepeople.loc.gov/contact (or main LoC contact form)
2. **Project Issues/Discussion:** GitHub repository (if open)
3. **Volunteer Coordination:** bythepeople.loc.gov typically has volunteer/contributor information

#### Collaboration Relevance
By the People / Concordia is the appropriate contact for:
- Understanding the current contribution/transcription intake process
- Exploring whether LoC-cleared items could be routed to By the People for volunteer transcription
- Verifying that the loc-public-domain-engine project does not duplicate or compete with existing efforts
- Establishing a feedback loop: our cleared items → By the People volunteers → corrected transcriptions → back to LoC/Hee-Lee Oss

### Outreach Status

- **Status:** NOT YET INITIATED  
- **Next Step:** Send introductory email (see template below)
- **Target Response Time:** 2-4 weeks
- **Follow-up:** If no response by [DATE], escalate or contact main LoC volunteer coordinator

#### Outreach Template: By the People / Concordia Introduction Email

```
Subject: Collaboration Inquiry — Public Domain Rights-Gate + Transcription Feed

To: [By the People/Concordia contact, TBD]
From: [Your name/Hee-Lee Oss]

Dear [By the People / Concordia team]:

I am reaching out on behalf of Hee-Lee Oss, a collaborative open-source initiative focused 
on public-good digital projects.

We are developing a **public-domain rights-gate and volunteer-friendly intake pipeline** 
(loc-public-domain-engine, https://github.com/Hee-Lee-Oss-Projects/loc-public-domain-engine) 
designed to:

1. **Identify and clear** affirmative public-domain/open-license items from the Library of Congress
2. **Feed verified, high-confidence items** into downstream good-deed projects, including 
   transcription and correction work
3. **Align rather than duplicate:** We want to ensure our effort complements (not competes with) 
   the excellent transcription work already happening in By the People / Concordia

**We are exploring whether:**
- Cleared LoC items could be routed to By the People for volunteer transcription
- There are existing pathways for external projects to contribute cleared-item feeds to 
  Concordia's intake
- We can establish a feedback loop: LoC items → Concordia volunteers → corrected transcriptions 
  → back to public archive

**Our goal is to reduce friction** for volunteers who want to contribute transcriptions: we 
do the rights-clearing and item discovery; you and your volunteers do the expert transcription 
work.

Would you have time for a brief conversation (15-30 minutes) to discuss this? We can 
accommodate any format (email, call, async) that works for your team.

Thank you for considering this outreach. I look forward to learning more about how we can 
align and support your mission.

Best regards,
[Your name]  
[Your email]  
[Project URL]  
[Phone (optional)]
```

### Outreach Record

**Outreach Attempt #1:**
- **Date Sent:** [TO BE RECORDED]
- **Method:** Email
- **Contact:** [NAME/EMAIL]
- **Response Status:** Awaiting response
- **Response Date:** [TO BE RECORDED]
- **Summary:** [TO BE RECORDED]
- **Engagement Status:** ☐ No response ☐ Received response ☐ In conversation ☐ Collaboration confirmed

**Follow-up Actions:**
- [ ] If no response after 2 weeks, resend with note: "Following up on the inquiry sent on [DATE]."
- [ ] If response received, log details and next steps below.

---

## Part 3: Rights Reviewer Appointment

### Role Definition

**Title:** Rights Reviewer (M0 Exit Criterion)

**Qualifications Required:**
- Demonstrated expertise in U.S. copyright law, public-domain status determination, and/or 
  intellectual property law
- Familiarity with Library of Congress, rightsstatements.org, and Creative Commons licensing
- Ability to read and provide feedback on legal/policy-heavy technical documentation
- Experience with or understanding of open-source cultural heritage / digital library projects
- Availability to review the `rights/vocabulary.yml` ruleset and adjudicate `needs-review` items 
  on an ongoing basis

**Responsibilities:**
1. **Ruleset Review:** Review and approve the `rights/vocabulary.yml` mapping that defines which 
   LoC/rightsstatements.org/Creative Commons metadata values map to "eligible" vs "ineligible" vs 
   "needs-review"
2. **Per-Item Adjudication:** Evaluate items flagged as "needs-review" by the gate and provide 
   a definitive rights determination (eligible/ineligible)
3. **Governance:** Hold veto authority over any item clearance; represent the legal/rights 
   dimension in Hee-Lee Oss governance discussions
4. **Documentation:** Document rationale for determinations and help refine the ruleset as 
   LoC metadata patterns or U.S. copyright law evolve

**Commitment Level:** 
- Initial: 8–16 hours (ruleset review + golden-test corpus review + CI gate sign-off)
- Ongoing: ~2–4 hours/month (adjudicating needs-review items + annual policy updates)

### Candidate Pool & Identification Strategy

#### Target Candidate Categories

1. **Academic IP/Copyright Specialists:**
   - Law professors specializing in copyright, cultural heritage, or digital libraries
   - Researchers at academic libraries focusing on digital collections / rights metadata
   - Potential contacts: 
     - Harvard Law School (Berkman Klein Center for Internet & Society)
     - Stanford Law School (Center for Internet and Society, Copyright Renewal Project)
     - University of Michigan (HathiTrust Digital Library, substantial LoC collaboration history)
     - University of Illinois / Library Research Center

2. **Library of Congress Staff:**
   - Rights/Metadata specialists within LoC itself (may have conflict of interest; to be evaluated)
   - Historical expertise in LoC's own rights determination processes
   - LoC Collections & Services division

3. **Professional Organization / Open-Source Community:**
   - **Wikimedia Foundation:** Extensive experience with public-domain determinations; may have 
     staff versed in rights metadata
   - **Internet Archive:** Operates similar rights-gating and provenance-tracking work; 
     institutional knowledge of public-domain challenges
   - **Creative Commons:** Maintain expertise in license determinations and open standards
   - **Open Source Initiative:** Governance and legal structures for collaborative projects
   - **Wikisource / Wikimedia Commons:** Community-based curation and rights determinations

4. **Pro-Bono / Public Interest Law:**
   - **Software Freedom Law Center:** Long track record advising open-source and public-benefit projects
   - **Public Knowledge:** Digital rights and policy organization
   - **Electronic Frontier Foundation (EFF):** Copyright and digital rights expertise
   - **National Endowment for the Humanities / National Humanities Alliance:** May have 
     recommendations for digital humanities / cultural heritage experts
   - **Library of Congress Foundation / Hee-Lee Oss existing counsel relationships**

#### Specific Candidate Research Notes

**For Rights Reviewer Role:**
- Consider reaching out to Wikimedia Foundation's legal/policy team; they have deep public-domain 
  expertise and may recommend a peer or volunteer
- University digital humanities centers (especially those running large digitization projects) 
  often employ or advise with rights specialists
- Academic publishers (O'Reilly, academic presses) have contracts/rights teams familiar with PD 
  determinations

**For Counsel/IP Attorney Role:**
- Software Freedom Law Center has provided pro-bono review to many open-source projects; 
  worth a direct inquiry
- Law school clinics (especially Berkman Klein at Harvard, Stanford's Center for Internet & Society) 
  may take on pro-bono review work
- Create Commons openly lists organizations and individuals experienced in open-licensing work

#### Recommended Outreach Targets (Priority Order)

**Priority 1 — Institutional Outreach (broader reach, higher likelihood of connection):**
- [ ] Wikimedia Foundation (rights/policy team) — ask for recommendation or direct interest
- [ ] Internet Archive (rights/metadata team) — established track record with similar projects
- [ ] Software Freedom Law Center — proven track record with open-source/public-benefit projects
- [ ] Library of Congress Foundation — may have existing counsel relationships or recommendations
- [ ] Hee-Lee Oss governance/board — leverage existing network and relationships

**Priority 2 — Academic/University Outreach:**
- [ ] Harvard Law School / Berkman Klein Center — email digital rights/IP faculty
- [ ] Stanford Law School / Center for Internet & Society — similar query
- [ ] University of Michigan Library / HathiTrust team — existing LoC relationship
- [ ] Local digital humanities centers — may know qualified reviewers

**Priority 3 — Direct Candidate Outreach (if names identified):**
- [ ] [Specific individual names to be added as candidates are identified during Priority 1-2 outreach]

#### Candidate Identification Process

- [ ] Reach out to Priority 1 institutional contacts (email templates provided below)
- [ ] Ask each organization: "Do you have someone on staff or in your network who would be 
      interested in serving as a rights reviewer / counsel for this project?"
- [ ] Collect names and reach out to identified candidates
- [ ] Post to Hee-Lee Oss community channels / governance for recommendations if Priority 1 
      yields no candidates
- [ ] If no qualified candidate emerges after 4 weeks, begin Priority 2 direct outreach
- [ ] If still no qualified candidate after 8 weeks total, escalate to Hee-Lee Oss board 
      with fallback procedure (Part 5)

#### Institutional Outreach Templates

**Template 1: To Wikimedia Foundation / Internet Archive**

```
Subject: Rights Reviewer + Counsel Recommendation Request — Public Domain Clearing Project

To: [Legal/Policy team contact]

Dear [Team name]:

I am reaching out on behalf of [Hee-Lee Oss] to ask for your guidance and possible recommendation.

We are developing a **public-domain rights-gate and API protocol** over the Library of Congress 
(loc-public-domain-engine, https://github.com/Hee-Lee-Oss-Projects/loc-public-domain-engine). 
The project uses a **deny-by-default rights-clearing ruleset** to identify affirmative PD/open-license 
items from LoC's collection and fans them into downstream good-deed work (transcription, alt-text, 
translation, datasets).

As part of our M0 milestone, we need to appoint:
1. A **qualified rights reviewer** to adjudicate borderline cases and approve our rights-vocabulary mapping
2. **Counsel or IP attorney** to review the legal soundness of the ruleset itself

Given your organization's deep expertise in public-domain determinations, open-licensing, and 
community curation, we would be grateful for:
- Recommendations of qualified individuals (on staff, in your network, or known experts) who might 
  be interested in serving in either role
- Any guidance on structuring rights review for this type of project

We can offer acknowledgment and appropriate attribution; we are also exploring pro-bono counsel 
pathways if budget constraints exist.

Would you have time for a brief conversation or email exchange about this? We're on a timeline 
to secure these roles by [DATE].

Thank you for considering this request. I look forward to hearing from you.

Best regards,
[Your name]  
[Email]  
[Phone]
```

**Template 2: To Law Schools / Academic Centers**

```
Subject: Rights Review Project — Seeking Expert Volunteer / Collaborator

To: [Berkman Klein Center / Stanford CIS / other center director or contact]

Dear [Director / Team name]:

I am writing to ask whether your organization might be interested in collaborating on a public-interest 
digital-rights project.

We are developing a **public-domain rights-gate** over the Library of Congress (loc-public-domain-engine) 
as part of the Hee-Lee Oss initiative. The project is designed to use a conservative, affirmative-determination-only 
approach to identify LoC items that are demonstrably public domain or openly licensed, and to fan them into 
downstream projects for transcription, alt-text, translation, and structured data.

We are seeking:
1. A **qualified rights reviewer** — someone with expertise in copyright law, public-domain status, and/or 
   digital heritage/library projects — to adjudicate borderline items and approve our core rights-vocabulary 
   ruleset
2. **Counsel or IP expertise** to provide legal review of the ruleset's soundness and defensibility

This could be structured as:
- A volunteer / pro-bono engagement (with acknowledgment and attribution)
- A student clinic project (if your institution has an IP law clinic)
- A faculty/researcher collaboration
- A flat-fee or hourly consulting arrangement

The initial review phase is 8–16 hours; ongoing work is ~2–4 hours/month.

Would your center or faculty be interested in exploring this? If so, I would be delighted to discuss 
how we might structure the collaboration.

Thank you for considering this inquiry. I look forward to hearing from you.

Best regards,
[Your name]  
[Email]  
[Phone]
```

**Template 3: To Software Freedom Law Center / Public Interest Law Organizations**

```
Subject: Pro-Bono Counsel Inquiry — Public Domain Rights-Clearing Project

To: [Legal Director or General Counsel contact]

Dear [Organization name]:

I am writing to inquire whether your organization might be able to provide pro-bono or low-cost 
legal review for a public-interest digital project.

We are developing the **loc-public-domain-engine** (https://github.com/Hee-Lee-Oss-Projects/loc-public-domain-engine), 
an open-source rights-gate and polite API protocol over the Library of Congress. The project identifies 
affirmative public-domain / openly-licensed items from LoC's collection and fans them into Hee-Lee Oss 
projects for transcription, alt-text, translation, and structured data — directly benefiting researchers, 
blind/low-vision users, speakers of low-resource languages, and digital humanists.

**We need legal review of:**
- Our rights-vocabulary mapping (the core ruleset that determines which LoC metadata values map to "clear" vs "needs human review" vs "ineligible")
- Liability/disclaimer language in our documentation to ensure users understand that we (not LoC) are making 
  the rights determination, and they bear their own due diligence

**Scope:** 
- Initial: 4–8 hours of attorney time (ruleset + documentation review)
- Ongoing: ~1–2 hours/month (advising on edge cases)

This project is pro-bono; we cannot pay large fees. However, it directly serves the public interest 
and aligns with digital-rights, open-access, and cultural-heritage missions.

Would your organization be interested in taking this on? If so, I would be happy to provide more 
details and propose a scope/fee structure.

Thank you for considering this request. I look forward to hearing from you.

Best regards,
[Your name]  
[Email]  
[Phone]
```

### Reviewer Appointment Record

**Nominated Candidate #1:**
- **Name:** [TO BE RECORDED]
- **Title/Affiliation:** [TO BE RECORDED]
- **Qualifications:** [TO BE RECORDED]
- **Contact Email:** [TO BE RECORDED]
- **Outreach Date:** [TO BE RECORDED]
- **Response Status:** ☐ Awaiting response ☐ Declined ☐ Accepted
- **Acceptance Date:** [TO BE RECORDED]
- **Notes:** [TO BE RECORDED]

**Nominated Candidate #2:**
[Repeat structure if needed]

**APPOINTED RIGHTS REVIEWER:**
- **Name:** [TO BE FILLED UPON ACCEPTANCE]
- **Title/Affiliation:** [TO BE FILLED UPON ACCEPTANCE]
- **Qualifications:** [TO BE FILLED UPON ACCEPTANCE]
- **Contact Email:** [TO BE FILLED UPON ACCEPTANCE]
- **Appointment Date:** [TO BE FILLED UPON ACCEPTANCE]
- **Ruleset Review Sign-Off:** ☐ Pending ☐ Complete (date: [TO BE RECORDED])

---

## Part 4: Counsel / IP Attorney Engagement

### Role Definition

**Title:** Counsel / Qualified Rights/IP Attorney (M0 Exit Criterion)

**Qualifications Required:**
- Licensed attorney with expertise in U.S. copyright law and intellectual property
- Familiarity with public-domain status, rights determinations, and open licensing
- Experience with or understanding of open-source projects, public-interest law, or cultural 
  heritage initiatives
- Ability to review and provide legal feedback on technical ruleset documentation

**Responsibilities:**
1. **Ruleset Legal Review:** Review the `rights/vocabulary.yml` mapping for legal soundness 
   and defensibility
2. **Disclaimer & Liability Review:** Review any public statements, documentation, or contracts 
   regarding the project's rights determinations to ensure proper liability disclaimers 
   ("Hee-Lee Oss makes the determination, not LoC; users bear their own legal due diligence")
3. **Risk Assessment:** Provide feedback on the deny-by-default gate's legal risk profile
4. **Governance:** Advise on any legal edge cases or governance decisions requiring legal perspective

**Commitment Level:**
- Initial: 4–8 hours (ruleset + documentation review + contract/disclaimer review)
- Ongoing: ~1–2 hours/month (advising on edge cases + annual legal updates due to rolling 
  U.S. PD dates or policy changes)

### Counsel Identification Strategy

#### Target Candidate Categories

1. **Public Interest / Open Source Law Firms:**
   - Software Freedom Law Center
   - Public Knowledge
   - Electronic Frontier Foundation (EFF)
   - National Library of Congress Foundation (or similar)

2. **Pro Bono / Academic:**
   - Law school clinics (IP law clinics, digital humanities clinics)
   - University counsel offices with public-interest mission
   - Law professors specializing in copyright

3. **Creative Commons / Open Source:**
   - Creative Commons has built expertise in open-license legal review
   - Open Source Initiative network may have recommendations

#### Engagement Process

- [ ] Reach out to Software Freedom Law Center with project overview
- [ ] Contact public-interest law firms for pro-bono recommendations or flat-fee review options
- [ ] Inquire with Creative Commons for referrals
- [ ] Contact Hee-Lee Oss governance to identify any existing counsel relationships
- [ ] Document hourly rate / engagement terms if not pro-bono

### Counsel Engagement Record

**Engagement Attempt #1:**
- **Firm/Contact:** [TO BE RECORDED]
- **Contact Email/Person:** [TO BE RECORDED]
- **Inquiry Date:** [TO BE RECORDED]
- **Response Status:** ☐ Awaiting response ☐ Declined ☐ Accepted
- **Response Date:** [TO BE RECORDED]
- **Engagement Terms:** [TO BE RECORDED: pro bono, hourly rate, flat fee, or other]
- **Notes:** [TO BE RECORDED]

**Engagement Attempt #2:**
[Repeat if needed]

**ENGAGED COUNSEL:**
- **Name/Firm:** [TO BE FILLED UPON ENGAGEMENT]
- **Contact Email/Person:** [TO BE FILLED UPON ENGAGEMENT]
- **Engagement Terms:** [TO BE FILLED UPON ENGAGEMENT]
- **Engagement Date:** [TO BE FILLED UPON ENGAGEMENT]
- **Ruleset Review Sign-Off:** ☐ Pending ☐ Complete (date: [TO BE RECORDED])

---

## Part 5: Fallback Procedure (If Reviewer or Counsel Seat Remains Empty)

**MANDATORY ESCALATION CLAUSE**

If, after 60 days of good-faith outreach, a qualified rights reviewer OR counsel cannot be 
secured:

### Escalation Procedure

1. **Documentation:** The project maintainer documents:
   - All outreach attempts (dates, contacts, responses received)
   - Reason for non-engagement (declined, unresponsive, unavailable, etc.)
   - A summary of efforts to find qualified candidates

2. **Escalation to Hee-Lee Oss Governance/Board:**
   - The maintainer presents the documentation to Hee-Lee Oss governance/board
   - The board decides on one of the following options:
     a. **Continue outreach:** Authorize further time / expanded search
     b. **Engage counsel:** Allocate budget to hire counsel on a paid basis
     c. **Defer M0 exit:** Postpone the milestone until a qualified reviewer/counsel is secured
     d. **Alternative governance:** Propose an alternate rights-review structure 
        (e.g., panel of reviewers, Hee-Lee Oss board review, external expert panel)

### Hard Gate During Empty Seat

**WHILE the reviewer or counsel seat is empty:**
- ☐ **No determination advances past `needs-review`**
- ☐ **No item is fanned out** from the rights-gate
- ☐ **M0 cannot exit** (hard criterion)
- ☐ **Escalation is active** — project is in governance review, not abandoned

This ensures the project never proceeds with rights determinations without proper expert 
oversight.

---

## Part 6: Consolidated Summary Table (To Be Updated)

| Item | Status | Name/Contact | Qualifications | Appointment/Response Date | Notes |
|------|--------|--------------|-----------------|---------------------------|-------|
| **LoC Labs Outreach** | Not initiated | TBD | N/A | TBD | See Part 1 |
| **By the People Outreach** | Not initiated | TBD | N/A | TBD | See Part 2 |
| **Rights Reviewer** | Open | TBD | TBD | TBD | See Part 3; hard M0 exit |
| **Counsel/IP Attorney** | Open | TBD | TBD | TBD | See Part 4; hard M0 exit |
| **Fallback Procedure** | Documented | N/A | N/A | N/A | See Part 5 |

---

## Part 7: Next Steps & Timeline

### Immediate Actions (Week 1)

- [ ] Update contact information for LoC Labs and By the People (verify URLs, find specific contact emails)
- [ ] Customize outreach email templates with project details and contact information
- [ ] Send LoC Labs outreach email
- [ ] Send By the People outreach email
- [ ] Begin candidate identification for Rights Reviewer (reach out to academic contacts, library organizations)
- [ ] Begin candidate identification for Counsel (reach out to public-interest law organizations)

### Ongoing Tracking (Weeks 2–8)

- [ ] Monitor for responses from LoC Labs and By the People outreach
- [ ] Follow up on outreach if no response after 2 weeks
- [ ] Document all responses and engagement status
- [ ] Record outreach outcomes honestly (response, no-response, in-conversation)

### Appointments (Weeks 4–8, or earlier if possible)

- [ ] Secure Rights Reviewer acceptance
- [ ] Secure Counsel/IP Attorney engagement
- [ ] Record qualifications and contact information

### Exit Criteria Fulfillment (Target: 60 days from outreach initiation)

- [ ] LoC Labs outreach status documented (Part 1 complete)
- [ ] By the People outreach status documented (Part 2 complete)
- [ ] Rights Reviewer named and appointed (Part 3 complete)
- [ ] Counsel/IP Attorney named and engaged (Part 4 complete)
- [ ] Fallback procedure documented (Part 5 complete and tested)
- [ ] This document committed to main branch via PR (Part 6 complete)
- [ ] M0 exit criteria (f) and (g) satisfied; M0 can exit

---

## Appendix: References

- **PLAN.md** — Project plan, Governance section, M0 exit criteria (f) and (g)
- **Library of Congress Labs:** https://labs.loc.gov/
- **By the People (Concordia):** https://bythepeople.loc.gov/
- **Library of Congress Contact:** https://loc.gov/contact
- **Hee-Lee Oss Governance:** (link to Hee-Lee Oss governance documentation)
- **Rights-vocabulary ruleset:** `rights/vocabulary.yml` (to be reviewed)

---

**Document License:** CC0-1.0 (per Hee-Lee Oss project output license)  
**Last Updated:** 2026-07-24  
**Status:** In Progress - Outreach to be initiated
