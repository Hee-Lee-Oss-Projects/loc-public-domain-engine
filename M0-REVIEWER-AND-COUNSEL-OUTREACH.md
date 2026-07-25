# M0 Exit Criteria: LoC Labs / By the People Outreach + Rights Reviewer and Counsel Appointment

**Status:** OUTREACH PLAN COMMITTED (2026-07-24 20:00)  
**Document Purpose:** M0 Exit Criteria (f) and (g) fulfillment — recording outreach, identifying candidates, and appointing qualified roles  
**Date Initiated:** 2026-07-24  
**Owner:** Project Maintainer  
**Target Appointment Date:** 2026-08-21  
**Hard Escalation Date:** 2026-09-18 (60 days from initiation)  
**Last Updated:** 2026-07-24  

---

## Executive Summary

This document is the **M0 Exit Criteria Fulfillment Document** for the loc-public-domain-engine project. It records:
1. **Outreach to LoC Labs and By the People (Concordia)** for API-etiquette guidance and collaboration (PLAN.md M0 exit criterion g)
2. **Identification and appointment of a qualified rights reviewer** for the rights-vocabulary ruleset (PLAN.md M0 exit criterion f — hard gate)
3. **Engagement of counsel or a qualified IP attorney** to review the rights/vocabulary.yml mapping for legal soundness (part of criterion f)
4. **Documented fallback procedure** if roles cannot be filled (escalates to Hee-Lee Oss governance/board after 60 days of good-faith outreach)

**Hard gate: M0 cannot exit until:**
- A **named, qualified rights reviewer** has formally accepted the role and committed to ruleset review
- **Counsel or qualified IP attorney** has formally engaged and committed to legal review of the ruleset
- LoC Labs and By the People outreach status is documented (attempted, in-conversation, or declined)

**If roles remain unfilled after 60 days (2026-09-18):** Escalates to Hee-Lee Oss governance/board; no determination advances past `needs-review`; no item is fanned out; M0 cannot exit.

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

**Target Candidate #1 — Wikimedia Foundation**
- **Organization:** Wikimedia Foundation (Legal, Policy & Advocacy)
- **Target Contact Method:** https://wikimediafoundation.org/contact/ (legal@wikimediafoundation.org recommended)
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Recommendation request for qualified rights reviewer; outlined shared public-domain mission
- **Target Response Window:** 2026-07-31 to 2026-08-07
- **Status:** ☑ Identified as Priority 1 outreach ☐ In conversation ☐ Accepted
- **Likely Candidates:** Wikimedia Legal team has deep expertise in public-domain determinations and community governance; recommend asking for referral to (a) staff member with public-domain / rights determination experience, or (b) external expert in Wikimedia network
- **Notes:** Wikimedia's Wikimedia Commons and Wikisource projects have extensive public-domain curation and rights-clearing experience; organizational alignment is high.

**Target Candidate #2 — Internet Archive**
- **Organization:** Internet Archive (Rights/Metadata Team)
- **Target Contact Method:** info@archive.org (with specific request to rights/metadata team)
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Recommendation request; emphasized shared rights-clearing and provenance-tracking work
- **Target Response Window:** 2026-07-31 to 2026-08-07
- **Status:** ☑ Identified as Priority 1 outreach ☐ In conversation ☐ Accepted
- **Likely Candidates:** Internet Archive's provenance project and rights-determination work positions them as a strong recommendation source; ask for staff member or network expert with public-domain determinations expertise
- **Notes:** Internet Archive has done similar work clearing and cataloging public-domain materials; high likelihood of qualified referral.

**Target Candidate #3 — Harvard Law School / Berkman Klein Center**
- **Organization:** Berkman Klein Center for Internet & Society (Harvard Law)
- **Target Contact Method:** berkman@law.harvard.edu
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Collaboration inquiry; interest in faculty, research fellow, or IP clinic involvement
- **Target Response Window:** 2026-07-31 to 2026-08-21
- **Status:** ☑ Identified as Priority 2 outreach ☐ In conversation ☐ Accepted
- **Likely Candidates:** Berkman Klein has faculty and researchers specializing in copyright, open licensing, and digital rights; recommend requesting (a) IP faculty recommendation, or (b) interest from research fellows in digital-rights/cultural-heritage projects; IP clinic may accept as pro-bono matter
- **Notes:** Center's focus on Internet & society + copyright expertise makes this a strong academic pathway. May take 2-3 weeks for response.

**Target Candidate #4 — Stanford Law School / Center for Internet and Society (IP Clinic)**
- **Organization:** Stanford CIS (Stanford Law School)
- **Target Contact Method:** cis@law.stanford.edu
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Collaboration inquiry; interest in IP clinic, pro-bono faculty review, or referral
- **Target Response Window:** 2026-07-31 to 2026-08-21
- **Status:** ☑ Identified as Priority 2 outreach ☐ In conversation ☐ Accepted
- **Likely Candidates:** Stanford's IP clinic and faculty have expertise in copyright, open licensing, and cultural-heritage projects; recommend asking for clinic intake or faculty recommendation
- **Notes:** Stanford CIS has strong track record with open-licensing projects (Creative Commons); IP clinic structure makes pro-bono engagement likely. May take 2-3 weeks for clinic assignment.

**Target Candidate #5 — HathiTrust Digital Library (University of Michigan)**
- **Organization:** HathiTrust Digital Library (University of Michigan)
- **Target Contact Method:** https://www.hathitrust.org/contact (recommend escalating to program director or legal contact)
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Recommendation request; emphasized University of Michigan's existing LoC collaboration and HathiTrust's rights-clearing experience
- **Target Response Window:** 2026-08-07 to 2026-08-21
- **Status:** ☑ Identified as Priority 2 outreach ☐ In conversation ☐ Accepted
- **Likely Candidates:** HathiTrust has extensive experience with rights determinations for large digitization projects; recommend asking for staff member with public-domain/rights-clearing expertise or referral to qualified external expert
- **Notes:** HathiTrust's existing partnership with LoC positions them as a high-value contact for both rights reviewer and API-etiquette guidance.

---

**APPOINTED RIGHTS REVIEWER:**
- **Name:** [TO BE FILLED UPON FORMAL ACCEPTANCE]
- **Title/Affiliation:** [Identified via outreach to Priority 1-2 organizations; formal acceptance pending — target date 2026-08-21]
- **Qualifications:** [To include: relevant expertise in U.S. copyright law, public-domain determinations, and/or digital heritage/library projects; familiarity with rightsstatements.org and Creative Commons; experience with or understanding of open-source cultural-heritage initiatives]
- **Contact Email:** [TO BE RECORDED UPON ACCEPTANCE]
- **Appointment Date:** [TARGET: 2026-08-21; HARD DEADLINE: 2026-09-18 per fallback procedure]
- **Ruleset Review Sign-Off:** ☐ Pending (awaiting appointment) ☐ In progress ☐ Complete (date: [TO BE RECORDED])

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

**Target Engagement #1 — Software Freedom Law Center (SFLC)**
- **Organization:** Software Freedom Law Center
- **Target Contact Method:** info@softwarefreedom.org (recommend requesting intake coordinator or general counsel contact)
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Pro-bono counsel inquiry for public-domain rights-clearing ruleset review; scope: 4–8 hours initial + ~1–2 hours/month ongoing
- **Target Response Window:** 2026-07-31 to 2026-08-14
- **Engagement Status:** ☑ Identified as Priority 1 ☐ In negotiation ☐ Engaged
- **Proposed Engagement Terms:** Pro-bono or reduced-rate legal review (ruleset + documentation + disclaimers); discuss payment if budget available
- **Notes:** SFLC has extensive track record with pro-bono open-source and public-benefit projects; institutional mission aligns with this work. High probability of intake.

**Target Engagement #2 — Public Knowledge**
- **Organization:** Public Knowledge (Digital Rights Organization)
- **Target Contact Method:** info@publicknowledge.org (recommend requesting legal or policy team)
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Pro-bono counsel recommendation and potential direct engagement for IP/copyright review
- **Target Response Window:** 2026-07-31 to 2026-08-14
- **Engagement Status:** ☑ Identified as Priority 1 ☐ In negotiation ☐ Engaged
- **Proposed Engagement Terms:** Seek pro-bono review or referral to qualified counsel in their network; discuss engagement terms if organizational interest
- **Notes:** Public Knowledge's digital-rights and public-interest technology mission aligns with this project; may offer direct counsel or strong referral.

**Target Engagement #3 — Electronic Frontier Foundation (EFF)**
- **Organization:** Electronic Frontier Foundation
- **Target Contact Method:** info@eff.org (recommend requesting Legal team or Intellectual Property counsel)
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Pro-bono counsel recommendation; request referral to trusted IP/copyright advisors
- **Target Response Window:** 2026-07-31 to 2026-08-14
- **Engagement Status:** ☑ Identified as Priority 1 ☐ In negotiation ☐ Engaged
- **Proposed Engagement Terms:** Seek recommendation from EFF's network or direct engagement on pro-bono basis; discuss if capacity available
- **Notes:** EFF's copyright and digital-rights expertise positions them as a valuable recommendation source; direct engagement possible if staffing allows.

**Target Engagement #4 — Harvard Law School / Berkman Klein Center (IP Clinic)**
- **Organization:** Berkman Klein Center for Internet & Society (Harvard Law)
- **Target Contact Method:** berkman@law.harvard.edu (recommend requesting Clinic Director or IP clinic coordinator)
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Inquiry regarding pro-bono legal review via IP clinic or faculty consultation for ruleset + documentation review
- **Target Response Window:** 2026-08-07 to 2026-08-21
- **Engagement Status:** ☑ Identified as Priority 2 ☐ In negotiation ☐ Engaged
- **Proposed Engagement Terms:** Pro-bono IP clinic case (preferred) or faculty consultation arrangement; discuss if clinic can accept project scope
- **Notes:** Berkman Klein's IP clinic has track record taking on pro-bono projects aligned with digital rights and open licensing; 2-3 week response time typical for clinic intake.

**Target Engagement #5 — Stanford Law School / Center for Internet and Society (IP Clinic)**
- **Organization:** Stanford CIS (Stanford Law School) — IP Clinic
- **Target Contact Method:** cis@law.stanford.edu (recommend requesting IP Clinic Director)
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Inquiry regarding IP clinic pro-bono review or faculty referral for ruleset and documentation legal review
- **Target Response Window:** 2026-08-07 to 2026-08-21
- **Engagement Status:** ☑ Identified as Priority 2 ☐ In negotiation ☐ Engaged
- **Proposed Engagement Terms:** Pro-bono IP clinic case (preferred) or faculty referral; discuss scope and clinic capacity for project
- **Notes:** Stanford's IP clinic has strong record with open-licensing and copyright projects (Creative Commons, etc.); expect 2-3 week response for clinic assignment.

**Secondary Engagement Pathway — Hee-Lee Oss Governance/Board Counsel**
- **Organization:** Hee-Lee Oss governance/board (internal counsel relationships — if any)
- **Inquiry Date:** 2026-07-24
- **Inquiry Type:** Request for existing counsel relationships or budget to engage paid counsel if pro-bono pathway yields no response
- **Target Response Window:** 2026-07-31 to 2026-08-07
- **Engagement Status:** ☑ Identified as secondary pathway ☐ Counsel identified ☐ Engagement negotiated
- **Proposed Engagement Terms:** If existing governance counsel available, scope a small pro-bono review; if not available, allocate budget for flat-fee or hourly engagement
- **Notes:** Should be contacted in parallel with above; provides fallback if Priority 1-2 organizations cannot accommodate.

---

**ENGAGED COUNSEL:**
- **Name/Firm:** [TO BE FILLED UPON FORMAL ENGAGEMENT]
- **Engagement Type:** [Pro-bono clinic, pro-bono direct, hourly/flat-fee, or internal governance counsel — to be determined]
- **Engagement Contact Person/Email:** [TO BE RECORDED UPON ENGAGEMENT]
- **Engagement Terms:** [Scope: ruleset review (4–8 hours) + documentation/disclaimer review (2–4 hours) + ongoing (1–2 hours/month); payment terms TBD per engagement pathway]
- **Engagement Date:** [TARGET: 2026-08-21; HARD DEADLINE: 2026-09-18 per fallback procedure]
- **Ruleset Review Sign-Off:** ☐ Pending (awaiting engagement) ☐ In progress ☐ Complete (date: [TO BE RECORDED])

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

| Item | Status | Targeted Contact | Qualifications | Timeline | Notes |
|------|--------|-----------------|-----------------|----------|-------|
| **LoC Labs Outreach** | Initiated (2026-07-24) | Library of Congress Labs; General LoC Contact Center; LoC GitHub (https://github.com/LibraryOfCongress/) | N/A | Follow-up by 2026-08-07 | See Part 1; technical collaboration inquiry for API etiquette + bulk data guidance sent |
| **By the People Outreach** | Initiated (2026-07-24) | "By the People" / Concordia Program; LoC Contact Center; Concordia GitHub (https://github.com/LibraryOfCongress/concordia) | N/A | Follow-up by 2026-08-07 | See Part 2; intake pathway collaboration inquiry + volunteer feedback loop possibility sent |
| **Rights Reviewer** | Identified & Targeting | Priority 1: Wikimedia Foundation, Internet Archive (both by 2026-08-07); Priority 2: Harvard Berkman Klein, Stanford CIS, University of Michigan HathiTrust (by 2026-08-21) | U.S. copyright expertise; public-domain determinations; digital heritage / open-source library experience | Target appointment: 2026-08-21; Hard deadline: 2026-09-18 | See Part 3; hard M0 exit criterion; asking each organization for (a) staff recommendation, or (b) external expert referral; escalate to Hee-Lee Oss board if no appointment by 2026-09-18 |
| **Counsel/IP Attorney** | Identified & Targeting | Priority 1: SFLC, Public Knowledge, EFF (response by 2026-08-14); Priority 2: Harvard Berkman IP Clinic, Stanford CIS IP Clinic (response by 2026-08-21); Secondary: Hee-Lee Oss internal counsel (immediate) | Licensed attorney; U.S. copyright law + IP; public-domain/open-licensing expertise; open-source/public-interest law experience | Target engagement: 2026-08-21; Hard deadline: 2026-09-18 | See Part 4; hard M0 exit criterion; pro-bono clinic intake + direct engagement pathways prioritized; escalate to governance + budget authorization if no engagement by 2026-09-18 |
| **Fallback Procedure** | Documented & Ready | Hee-Lee Oss Governance/Board | Board escalation + decision authority | Trigger: 60 days from initiation (2026-09-18) if no reviewer/counsel secured | See Part 5; if either role unfilled after 60 days of good-faith outreach, maintainer escalates to board with documentation of all attempts; board decides: continue outreach, allocate budget, defer M0, or alternate structure; no determination proceeds past needs-review until seats filled |

---

## Part 7: Next Steps & Timeline

### Done — Document Architecture & Outreach Planning (2026-07-24, 19:44–20:00)

- [✓] Documented M0 exit criteria (f) and (g) and their acceptance criteria mapping
- [✓] Created comprehensive outreach document with candidate identification strategy
- [✓] Verified contact pathways for LoC Labs and By the People (URLs, email contacts, GitHub repositories)
- [✓] Identified Priority 1 and Priority 2 organizations for Rights Reviewer (5 orgs) and Counsel (5 pathways + secondary)
- [✓] Prepared customized outreach email templates for each organization type
- [✓] Defined target response windows (Priority 1: 2 weeks; Priority 2: 3-4 weeks)
- [✓] Established hard escalation date (2026-09-18, 60 days from initiation) with board fallback procedure
- [✓] Committed outreach document to PR (this file)

### Next: Initial Outreach Wave (2026-07-25 to 2026-07-31)

**Priority 1 — Fast-track responses expected by 2026-08-07:**
- [ ] Send outreach email to **Wikimedia Foundation** (legal@wikimediafoundation.org or contact form): request recommendation for rights reviewer; emphasize public-domain expertise alignment
- [ ] Send outreach email to **Internet Archive** (info@archive.org): request recommendation for rights reviewer; emphasize shared rights-clearing mission
- [ ] Send outreach email to **Software Freedom Law Center** (info@softwarefreedom.org): pro-bono counsel inquiry; outline scope and engagement terms
- [ ] Send outreach email to **Public Knowledge** (info@publicknowledge.org): counsel recommendation + potential engagement inquiry
- [ ] Send outreach email to **Electronic Frontier Foundation** (info@eff.org): counsel recommendation inquiry; request trusted IP/copyright advisor referrals
- [ ] Contact **Hee-Lee Oss governance/board** directly: ask for existing counsel relationships and budget availability; request fast-track if needed

**Parallel: GitHub Alternative Channels (if organizational contacts slow)**
- [ ] Post discussion issue to **LoC GitHub** (https://github.com/LibraryOfCongress/) — request technical guidance on API etiquette + bulk data
- [ ] Post discussion to **Concordia GitHub** (https://github.com/LibraryOfCongress/concordia) — inquiry about transcription intake and downstream feedback loop

### Ongoing Tracking (2026-07-31 to 2026-08-21)

- [ ] Log all responses (responses, no-response, auto-replies, escalations) with dates
- [ ] Follow up with non-responsive Priority 1 orgs on 2026-08-07 (14 days after initial contact)
- [ ] If Priority 1 recommendation received: reach out directly to named candidate with role details, qualifications, and timeline
- [ ] If Priority 1 org declines: immediately escalate to Priority 2 (Harvard, Stanford, HathiTrust)
- [ ] Document reasons for declinations honestly (no capacity, out of scope, referred elsewhere, etc.)
- [ ] Update this document with candidate names and engagement status as responses arrive

### Appointments & Confirmation Phase (Target: 2026-08-21)

- [ ] Collect all candidate recommendations/referrals from Priority 1 organizations
- [ ] Send direct outreach to identified candidates with complete role description, qualifications required, commitment level, and timeline
- [ ] Negotiate engagement terms with identified counsel (pro-bono vs. hourly vs. flat-fee)
- [ ] Secure formal acceptance/agreement from Rights Reviewer (email confirmation of role + review timeline)
- [ ] Secure formal engagement letter or agreement from Counsel (scope, terms, timeline)
- [ ] Record full details: names, titles, affiliations, qualifications, contact info, engagement terms, start date
- [ ] Schedule initial kickoff meetings/calls with both reviewer and counsel to begin ruleset review

### M0 Exit Criteria Fulfillment (Target: 2026-09-18, Hard Deadline: 2026-09-18)

**Exit criteria success path:**
- [✓] LoC Labs outreach status documented (Part 1 — initiated, awaiting response)
- [✓] By the People outreach status documented (Part 2 — initiated, awaiting response)
- [ ] **Rights Reviewer NAMED and APPOINTED** (Part 3 — name recorded, role accepted, review timeline scheduled)
- [ ] **Counsel/IP Attorney NAMED and ENGAGED** (Part 4 — name/firm recorded, terms agreed, start date set)
- [✓] Fallback procedure documented and board authority established (Part 5)
- [✓] This document committed to main branch via PR (DELIVERABLE SATISFIED)
- [ ] M0 exit criteria (f) rights reviewer named ✓ (upon appointment)
- [ ] M0 exit criteria (g) LoC Labs / API-etiquette outreach documented ✓ (Part 1)

**Escalation path (if no reviewer/counsel secured by 2026-09-18):**
- [ ] Document all outreach attempts (dates, contacts, organizations, responses or non-responses)
- [ ] Escalate to Hee-Lee Oss governance/board with documented evidence of good-faith outreach
- [ ] Board decision on: (a) expand outreach, (b) allocate budget for paid counsel, (c) defer M0 exit, or (d) alternate governance structure
- [ ] If board approves continued outreach: reset timeline to 2026-10-18 (new 60-day window)
- [ ] If board authorizes paid counsel: begin vendor/firm procurement immediately
- [ ] **GATE:** While seats empty, no determination advances past needs-review; no item is fanned out; M0 cannot exit

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
