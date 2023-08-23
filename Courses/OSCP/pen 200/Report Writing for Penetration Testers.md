
https://portal.offsec.com/courses/pen-200/books-and-videos/modal/modules/report-writing-for-penetration-testers/writing-effective-technical-penetration-testing-reports/executive-summary
## What do I want to know?

1.  How much content do I need to collect i.e.do I need to screen capture everyting?
2.  What do I need to note as I'm going?
3. What is the method that is applied consistently?
4. What does get of jail for free look like and how is it provided?
## Penetration Testing Deliverables

Important to define the scope of the engagement before starting.  This is important so that it is clear what is and isn't in scope of the engagement.

## Note portability

Good notes are essential in developing a 'penetration testing report'.  It is essential that test processes and steps can be reproduced if required.  Notes need to be able to be searched, shared and replicated if required.

Effective notes permits team members to support each other should that be required.

## General structure of notes

Everything we do should be recorded.  Notes, commands, changes to code, links selected e.t.c.

Notes need to ensure that we can use them to repeat what we have done.  

> If others cannot use your notes to replicate what has been done they are essentially useless.

## Writing Effective Technical Penetration Testing Reports

Important aspects of a technical report includes the purpose of the report and that it is provided in such a manner that the client understands it.

It is important to understand their business goals and objectives.  It also important to understand the types of information security risks that their industry.

## Technical Summary

This section contains a list of the key findings in the report written out with a summary and recommendations for a technical person.  

This section should group findings into common areas.  The structure of this section might follow this sort of pattern:

1. User and privilege management;
2. Architecture;
3. Authorisation;
4. Patch Management;
5. Integrity and signatures;
6. Authentication;
7. Access Control;
8. Audit, log management and monitoring;
9. Traffic and data encryption; and
10. Security misconfigurations.

An example of a technical summary:

![[tech_summary.png]]

This section should finish with a risk heat-map based on vulnerability severity adjusted as appropriate to the client's context, and as agreed upon a client security risk representative if possible.

## [Technical Findings and Recommendations](https://portal.offsec.com/courses/pen-200/books-and-videos/modal/modules/report-writing-for-penetration-testers/writing-effective-technical-penetration-testing-reports/technical-findings-and-recommendation)

This is where we document the full technical details relating to the pen test (engagement), including what we consider to be appropriate steps for remediation.  Whilst this is a technical section, we should not assume that those who are reading this document that they understand the nuances of vulnerabilities.

This section is often presented in tabular format and explains our findings.  A finding might cover just one vulnerability or cover multiple vulnerabilities of the same type.

It is important to note that there may be a requirement for a 'attack narrative' .  The narrative is in story format and explains what  happened during the test.

|Reference|Risk|Description and Implications|Recommendations|
|---------|----|----------------------------|---------------|
|1|H|Account, password and privilege management|All accounts should have passwords that are enforced by a slick policy|

With regard to risk assessments, its important to differentiate between technical risk and business context risk.  Different industries and business will prioritise different things.  For example some businesses value patching over availability.  This aspect could influence the calculation of overall risk.  

> The value in understanding the business context and priorities cannot be overstated.  The engagement must understand and focus on the business need.  Penetration tests should inform the business of any aspects that are generally important but largely unknown to the business.  That is to say, that the business aspects will guide the engagement, however, as experts in penetration testing we should ensure that this experience ensure s thorough test.

It is fundamentally important that what we present as vulnerabilities and remediation's can be replicated as required.

Each vulnerability should be described in the following way:

1. The affected URL/endpoint; and
2. A method of triggering the vulnerability.
## Tailor the content

The audience for a technical report may include those who are not technical, consequently the report needs to include business relevant information.  This may include business risk, mitigation, and costs/effort to rectify and maintain.

## Executive summary

The executive summary should clearly highlight what was and wasn't in scope, especially when a large number of vulnerabilities.  This is to protect the pen tester from criticism if the additional work meant that they didn't have the budget/time to complete all the in-scope work.

Ideally, we want group findings with similar vulnerabilities.

It is important to highlight aspects that the client is doing well.

## Testing environment considerations

It is important to document the testing environment  and any circumstances that cause a change to the environment.

There are three states which need to be considered with extenuation circumstances:

1. Positve outcome: There were no limitations or extenuating circumstances in the engagement.  The time allocated was sufficient to thoroughly test the environment;
2. Neutral outcome:  There were no credentials allocated to the tester in the first two days of the test.  However, the attack surface was much smaller than anticipated.  Therefore, this did not have an impact on the overall test.  Offsec recommends that communication of credentials occurs immediately before the engagement begins for future contracts, so that we can provide as much testing as possible within the allocated time.
3. Negative outcome:  There was not enough time allocated to this engagement to conduct a thorough review of the application, and the scope became much larger than expected.  It is recommended that more time is allocated to future engagements to provide more comprehensive coverage.

## Appendices, further information and references.

Things that go here generally don't have a spot in the main part of the report.  This could include long lists of enumerated users, large code blocks, expanded methodology or technical write-ups

## Document Structure

### Front matter

### Table of Comments

### List of figures
### Scope 

### Rules of Engagement

### Stakeholders

### Deliverables

### Schedule

### Executive

### Testing Environment

### Technical Summary

### Technical Findings and Recommendations

### Appendices, Further Information and References 

## Raw notes

- Whilst a specific set of steps can not be defined at the beginning of an engagement, a consistent method can be established and followed.  The specifics need to be developed during the engagement.
- Some engagements will be undertaken with no details of the environment provided.  This provides a much more realistic engagement.  However, it takes longer and will be more expensive.  In this scenario very little planning can be undertaken before the engagement.  The opposite might include the customer might provide the details of what machines are to be tested.
- In instances where little detail is provided, a detailed plan cannot be developed.  Instead, 'pen testers' rely on detailed notes and record of what steps are taken.
- These steps mean that:
	- The penetration test can be repeated if required;
	- Any issues can be patched/fixed; and
	- If there is a system failure during the penetration, the client and the 'pen tester' can determine if the steps taken in the engagement caused the outage.

- During an engagement, some tests may not be permitted, consequently we must be sure on the 'rules of engagement'.
- When using screenshots, it is important that they are intuitive by themselves and require little text to understand the.
- Note should be concise and precise
### Example note
For a web application vulnerability, a note might take the following structure:

1. Application name;
2. URL;
3. Request type;
4. Issue detail; and
5. Proof of Concept Payload.

----
Testing for Cross-Site Scripting

Testing target:  192.168.1.52
Application:  XSSBlog
Date Started: 31 March 2022

1.  Navigated to the application 'http://192.168.1.52/XSSBlog.html'
	1. Result:  Blog page loaded as expected.
2. Entered our standard XSS test data:
	1. You will rejoice to hear that no disaster has accompanied the commencement of an enterprise which you have regarded with such evil forebodings.<script>alert("Your computer is infected!");</script>I have arrived here yesterday, and my first task is to assure my dear sister of my welfare and increasing confidence in the success of my undertaking.
3. Clicked submit to post the blog entry.
	1. Result: Blog entry appeared to save correctly.
4. Navigated to read the blog post 'http://192.168.1.52/XSSRead.php'
	1. Result:  The blog started to display and then the expected alert popped up.
5. Test indicated the site is vulnerable to XSS.

PoC payload:  <script>alert("Your computer is infected!")</script>

----
## Inserting images

![[test_image_oscp.png]]

## Follow up

## Tags
#notes
#rulesofengagement
#scope
#report
#getoutofjailfree
#pentestingmetho
#planning
#constraints
#OWASPPenTestingExecutionStandard
#generalnotestructure
#screenshots
#insertimage
#desireablepropertise
#concise
#precise
#purpose
#reportcontent
#executivesummary
#positiveoutcome
#neutraloutcome
#negativeoutcome

