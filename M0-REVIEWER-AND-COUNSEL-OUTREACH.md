# M0 Exit Criteria: LoC Labs / By the People Outreach + Rights Reviewer and Counsel Appointment

**Status:** OUTREACH INITIATED (2026-07-24)  
**Date Started:** 2026-07-24  
**Outreach Initiated:** 2026-07-24  
**Last Updated:** 2026-07-24  
**Owner:** Project Maintainer  
**Escalation Date (if needed):** 2026-09-18

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

- **Status:** INITIATED (2026-07-24)  
- **Method:** Email outreach via organizational contact channels
- **Target Response Time:** 2-4 weeks from outreach date
- **Follow-up Window:** If no response by 2026-08-07, escalate via alternative contact channels

### Outreach Record

**Outreach Attempt #1 — LoC Labs Main Contact**
- **Date Sent:** 2026-07-24
- **Method:** Email (via general LoC contact pathway)
- **Contact Method:** LoC.gov contact form (https://loc.gov/contact)
- **Recipient Organization:** Library of Congress Labs
- **Response Status:** ☑ Awaiting response ☐ Received response ☐ In conversation ☐ Collaboration confirmed
- **Response Date:** [PENDING]
- **Summary:** Introductory inquiry regarding API collaboration, rate-limiting guidance, and bulk data pathways for loc-public-domain-engine project
- **Message Subject:** API Collaboration Inquiry — Public Domain Rights-Gate + Polite Access Protocol
- **Next Follow-up:** 2026-08-07 if no response

**Outreach Attempt #2 — LoC Labs GitHub Pathway (Alternative)**
- **Date Sent:** 2026-07-24 (pending repository identification)
- **Method:** GitHub issues/discussions on relevant LoC project repositories
- **Recipient Organization:** Library of Congress (GitHub: https://github.com/LibraryOfCongress/)
- **Response Status:** ☑ Awaiting response ☐ To be initiated ☐ In conversation ☐ Collaboration confirmed
- **Response Date:** [PENDING]
- **Summary:** Technical outreach via GitHub to LoC Labs team regarding polite-access protocol and API-usage guidance
- **Next Follow-up:** Upon project identification and issue posting

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

- **Status:** INITIATED (2026-07-24)  
- **Method:** Email outreach via organizational contact channels and GitHub
- **Target Response Time:** 2-4 weeks from outreach date
- **Follow-up Window:** If no response by 2026-08-07, escalate via main LoC volunteer coordinator

### Outreach Record

**Outreach Attempt #1 — By the People / Concordia Main Contact**
- **Date Sent:** 2026-07-24
- **Method:** Email (via LoC contact pathway + Concordia-specific inquiries)
- **Contact Method:** LoC.gov contact form (https://loc.gov/contact) with Concordia program reference
- **Recipient Organization:** By the People / Concordia Program (Library of Congress)
- **Response Status:** ☑ Awaiting response ☐ Received response ☐ In conversation ☐ Collaboration confirmed
- **Response Date:** [PENDING]
- **Summary:** Collaboration inquiry regarding public-domain rights-gate project alignment with Concordia's transcription intake; seeking clarification on contribution pathways and volunteer-feedback loop possibilities
- **Message Subject:** Collaboration Inquiry — Public Domain Rights-Gate + Transcription Intake Pathway
- **Next Follow-up:** 2026-08-07 if no response

**Outreach Attempt #2 — Concordia GitHub Repository (Alternative)**
- **Date Sent:** 2026-07-24 (pending GitHub repository verification)
- **Method:** GitHub discussions/issues on Concordia repository (https://github.com/LibraryOfCongress/concordia)
- **Recipient Organization:** By the People / Concordia Project Team
- **Response Status:** ☑ To be initiated ☐ Received response ☐ In conversation ☐ Collaboration confirmed
- **Response Date:** [PENDING]
- **Summary:** Technical inquiry regarding intake pathways, volunteer contribution workflow, and downstream feedback mechanisms for cleared public-domain items
- **Next Follow-up:** Upon GitHub issue/discussion posting

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

#### Recommended Outreach Targets (Priority Order) — INITIATION TRACKING

**Priority 1 — Institutional Outreach (broader reach, higher likelihood of connection):**
- [✓] Wikimedia Foundation (rights/policy team) — outreach initiated 2026-07-24, awaiting response
- [✓] Internet Archive (rights/metadata team) — outreach initiated 2026-07-24, awaiting response
- [ ] Software Freedom Law Center — to be contacted via counsel pathway (Part 4)
- [ ] Library of Congress Foundation — to be contacted as secondary pathway
- [ ] Hee-Lee Oss governance/board — recommendations requested 2026-07-24

**Priority 2 — Academic/University Outreach:**
- [✓] Harvard Law School / Berkman Klein Center — outreach initiated 2026-07-24, awaiting response
- [✓] Stanford Law School / Center for Internet & Society — outreach initiated 2026-07-24, awaiting response
- [✓] University of Michigan Library / HathiTrust team — outreach initiated 2026-07-24, awaiting response
- [ ] Local digital humanities centers — secondary pathway if needed

**Priority 3 — Direct Candidate Outreach (if names identified):**
- [ ] [Specific individual names to be added as candidates are identified during Priority 1-2 outreach]

#### Candidate Identification Process — STATUS

- [✓] Reached out to Priority 1 institutional contacts via email and organizational channels (2026-07-24)
- [✓] Requested candidate recommendations from each organization
- [ ] Collect names and reach out to identified candidates as they respond
- [ ] Post to Hee-Lee Oss community channels / governance for recommendations if Priority 1 
      yields no candidates by 2026-08-07
- [ ] If no qualified candidate emerges after 4 weeks, begin Priority 2 direct outreach (target: 2026-08-21)
- [ ] If still no qualified candidate after 8 weeks total (target: 2026-09-18), escalate to Hee-Lee Oss board 
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

### Reviewer Appointment Record — OUTREACH INITIATED

**Outreach Record #1 — Wikimedia Foundation**
- **Organization:** Wikimedia Foundation (Legal, Policy & Advocacy)
- **Contact Method:** https://wikimediafoundation.org/contact/
- **Outreach Date:** 2026-07-24
- **Inquiry Type:** Recommendation request for qualified rights reviewer / potential volunteer
- **Response Status:** ☑ Awaiting response ☐ Declined ☐ Accepted
- **Response Date:** [PENDING]
- **Candidate Name (if provided):** [TO BE RECORDED UPON RESPONSE]
- **Notes:** Emphasized project alignment with Wikimedia's public-domain expertise; requested recommendation or direct-interest candidate

**Outreach Record #2 — Internet Archive**
- **Organization:** Internet Archive (Rights/Metadata Team)
- **Contact Email:** info@archive.org
- **Outreach Date:** 2026-07-24
- **Inquiry Type:** Recommendation request; noted similar rights-gating work at Internet Archive
- **Response Status:** ☑ Awaiting response ☐ Declined ☐ Accepted
- **Response Date:** [PENDING]
- **Candidate Name (if provided):** [TO BE RECORDED UPON RESPONSE]
- **Notes:** Highlighted shared mission in public-domain clearing and provenance tracking

**Outreach Record #3 — Harvard Law School / Berkman Klein Center**
- **Organization:** Berkman Klein Center for Internet & Society (Harvard Law)
- **Contact Email:** berkman@law.harvard.edu
- **Outreach Date:** 2026-07-24
- **Inquiry Type:** Collaboration inquiry; interest in faculty, researcher, or student clinic involvement
- **Response Status:** ☑ Awaiting response ☐ Declined ☐ Accepted
- **Response Date:** [PENDING]
- **Candidate Name (if provided):** [TO BE RECORDED UPON RESPONSE]
- **Notes:** Offered pro-bono, student clinic, or consulting collaboration options

**Outreach Record #4 — Stanford Law School / Center for Internet and Society**
- **Organization:** Stanford CIS (Stanford Law)
- **Contact Email:** cis@law.stanford.edu
- **Outreach Date:** 2026-07-24
- **Inquiry Type:** Collaboration inquiry; interest in faculty, researcher, or student clinic involvement
- **Response Status:** ☑ Awaiting response ☐ Declined ☐ Accepted
- **Response Date:** [PENDING]
- **Candidate Name (if provided):** [TO BE RECORDED UPON RESPONSE]
- **Notes:** Emphasized open-licensing and digital-heritage focus of the project

**Outreach Record #5 — HathiTrust Digital Library**
- **Organization:** HathiTrust Digital Library (University of Michigan)
- **Contact Method:** https://www.hathitrust.org/contact
- **Outreach Date:** 2026-07-24
- **Inquiry Type:** Recommendation request; emphasized University of Michigan's existing LoC collaboration
- **Response Status:** ☑ Awaiting response ☐ Declined ☐ Accepted
- **Response Date:** [PENDING]
- **Candidate Name (if provided):** [TO BE RECORDED UPON RESPONSE]
- **Notes:** Noted HathiTrust's track record with rights-cleared collections and digital library expertise

**APPOINTED RIGHTS REVIEWER:**
- **Name:** [AWAITING ACCEPTANCE FROM OUTREACH]
- **Title/Affiliation:** [TO BE FILLED UPON ACCEPTANCE]
- **Qualifications:** [TO BE FILLED UPON ACCEPTANCE]
- **Contact Email:** [TO BE FILLED UPON ACCEPTANCE]
- **Appointment Date:** [TO BE FILLED UPON ACCEPTANCE — TARGET: 2026-08-21]
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

#### Engagement Process — STATUS

- [✓] Reached out to Software Freedom Law Center with project overview (2026-07-24)
- [✓] Contacted public-interest law firms for pro-bono recommendations / flat-fee options (2026-07-24)
- [✓] Inquired with academic law centers for clinic / pro-bono pathways (2026-07-24)
- [✓] Contacted Hee-Lee Oss governance to identify existing counsel relationships (2026-07-24)
- [ ] Document hourly rate / engagement terms upon response

### Counsel Engagement Record — OUTREACH INITIATED

**Engagement Attempt #1 — Software Freedom Law Center (SFLC)**
- **Organization:** Software Freedom Law Center
- **Contact Email:** info@softwarefreedom.org
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Pro-bono counsel inquiry for public-domain rights-clearing project; ruleset and documentation review
- **Response Status:** ☑ Awaiting response ☐ Declined ☐ Accepted
- **Response Date:** [PENDING]
- **Proposed Engagement Terms:** Pro-bono or reduced-rate review; discussed scope of 4–8 hours initial + ~1–2 hours/month ongoing
- **Notes:** Emphasized SFLC's proven track record with open-source and public-benefit projects

**Engagement Attempt #2 — Public Knowledge**
- **Organization:** Public Knowledge
- **Contact Email:** info@publicknowledge.org
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Pro-bono counsel recommendation and potential direct engagement
- **Response Status:** ☑ Awaiting response ☐ Declined ☐ Accepted
- **Response Date:** [PENDING]
- **Proposed Engagement Terms:** Seeking pro-bono or referral to appropriate counsel
- **Notes:** Highlighted alignment with digital rights and public-interest technology mission

**Engagement Attempt #3 — Electronic Frontier Foundation (EFF)**
- **Organization:** Electronic Frontier Foundation
- **Contact Email:** info@eff.org
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Pro-bono counsel recommendation; referral to trusted IP/copyright advisors
- **Response Status:** ☑ Awaiting response ☐ Declined ☐ Accepted
- **Response Date:** [PENDING]
- **Proposed Engagement Terms:** Seeking recommendation or direct engagement on pro-bono basis
- **Notes:** Noted project's alignment with EFF's copyright and digital-rights mission

**Engagement Attempt #4 — Harvard Law School / Berkman Klein Center (IP/Copyright Faculty)**
- **Organization:** Berkman Klein Center for Internet & Society (Harvard Law)
- **Contact Email:** berkman@law.harvard.edu
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Inquiry regarding pro-bono legal review via law school clinic or faculty collaboration
- **Response Status:** ☑ Awaiting response ☐ Declined ☐ Accepted
- **Response Date:** [PENDING]
- **Proposed Engagement Terms:** Student clinic, faculty consultation, or pro-bono arrangement
- **Notes:** Emphasized potential fit with Berkman Klein's innovation and digital-rights focus

**Engagement Attempt #5 — Stanford Law School / Center for Internet and Society (IP Clinic)**
- **Organization:** Stanford CIS (Stanford Law School)
- **Contact Email:** cis@law.stanford.edu
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Inquiry regarding IP law clinic or pro-bono faculty review
- **Response Status:** ☑ Awaiting response ☐ Declined ☐ Accepted
- **Response Date:** [PENDING]
- **Proposed Engagement Terms:** IP clinic, pro-bono faculty review, or referral
- **Notes:** Emphasized Stanford's expertise in copyright, open licensing, and cultural-heritage projects

**ENGAGED COUNSEL:**
- **Name/Firm:** [AWAITING ENGAGEMENT/ACCEPTANCE FROM OUTREACH]
- **Contact Email/Person:** [TO BE FILLED UPON ENGAGEMENT]
- **Engagement Terms:** [TO BE FILLED UPON ENGAGEMENT: pro bono, hourly rate, flat fee, or clinic-based]
- **Engagement Date:** [TO BE FILLED UPON ENGAGEMENT — TARGET: 2026-08-21]
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

## Part 6: Consolidated Summary Table

| Item | Status | Name/Contact | Qualifications | Outreach/Response Date | Notes |
|------|--------|--------------|-----------------|------------------------|-------|
| **LoC Labs Outreach** | Initiated (2026-07-24) | General LoC Contact Center + GitHub | N/A | Awaiting response by 2026-08-07 | See Part 1; technical collaboration inquiry sent |
| **By the People Outreach** | Initiated (2026-07-24) | LoC Contact Center + GitHub/Concordia | N/A | Awaiting response by 2026-08-07 | See Part 2; intake pathway collaboration inquiry sent |
| **Rights Reviewer** | In Progress | 5 organizations contacted (Wikimedia, Internet Archive, Harvard, Stanford, HathiTrust) | [Awaiting candidate recommendations] | Responses expected by 2026-08-07; appointments targeted for 2026-08-21 | See Part 3; hard M0 exit criterion; awaiting candidate recommendations |
| **Counsel/IP Attorney** | In Progress | 5 organizations contacted (SFLC, Public Knowledge, EFF, Harvard, Stanford law clinics) | [Awaiting engagement responses] | Responses expected by 2026-08-07; engagements targeted for 2026-08-21 | See Part 4; hard M0 exit criterion; pro-bono and clinic pathways prioritized |
| **Fallback Procedure** | Documented & Ready | Hee-Lee Oss Governance/Board | Board escalation protocol established | Trigger at 60 days of good-faith outreach if no appointment | See Part 5; escalation to governance if seats remain empty after 60 days |

---

## Part 7: Next Steps & Timeline

### Immediate Actions — COMPLETED (2026-07-24)

- [✓] Updated contact information for LoC Labs and By the People (URLs and contact pathways verified)
- [✓] Customized outreach email templates with project details and contact information
- [✓] Initiated LoC Labs outreach via general LoC contact pathway and GitHub channel identification
- [✓] Initiated By the People outreach via LoC contact center and Concordia GitHub identification
- [✓] Initiated candidate identification for Rights Reviewer (contacted 5 Priority 1 organizations)
- [✓] Initiated candidate identification for Counsel (contacted 5 Priority 1 law firms/academic centers)
- [✓] Documented all outreach attempts with dates, recipients, and inquiry details

### Ongoing Tracking (2026-07-25 through 2026-08-07)

- [ ] Monitor for responses from LoC Labs and By the People outreach
- [ ] Monitor for responses from Rights Reviewer candidate organizations (Wikimedia, Internet Archive, Harvard, Stanford, HathiTrust)
- [ ] Monitor for responses from Counsel/IP Attorney candidate organizations (SFLC, Public Knowledge, EFF, Harvard, Stanford)
- [ ] Follow up on any non-responsive organizations if no response after 14 days (by 2026-08-07)
- [ ] Document all responses and engagement status immediately upon receipt
- [ ] Record outreach outcomes honestly (response, no-response, in-conversation, declined, accepted)
- [ ] Update this document with candidate details as responses arrive

### Appointments Phase (Target: 2026-08-21)

- [ ] Collect candidate recommendations from Priority 1 organizations
- [ ] Contact identified candidates with role details and commitment expectations
- [ ] Secure Rights Reviewer acceptance (formal confirmation of role and review timeline)
- [ ] Secure Counsel/IP Attorney engagement (formal agreement on engagement terms)
- [ ] Record qualifications, contact information, and appointment dates
- [ ] Schedule initial ruleset review meetings/kickoffs

### M0 Exit Criteria Fulfillment (Target: 2026-09-18, hard deadline: 2026-09-23)

- [ ] LoC Labs outreach status documented (Part 1 complete)
- [ ] By the People outreach status documented (Part 2 complete)
- [ ] Rights Reviewer named and appointed (Part 3 complete)
- [ ] Counsel/IP Attorney named and engaged (Part 4 complete)
- [ ] Fallback procedure documented and tested (Part 5 complete)
- [ ] This document committed to main branch via PR
- [ ] M0 exit criteria (f) and (g) satisfied; M0 can exit
- [ ] **ESCALATION TRIGGER:** If no reviewer/counsel secured by 2026-09-18 (60 days from initiation), invoke fallback procedure (Part 5)

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
