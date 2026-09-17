Google Dorking / Advanced Google Search — 2026 Field Guide
> **Purpose:** A practical, beginner-friendly and advanced reference for Google search operators used in OSINT, cybersecurity reconnaissance, defensive exposure assessment, research, and website troubleshooting.
>
> **Authorization rule:** Search only information you are legally permitted to investigate. Do not use search operators to target private individuals, obtain credentials, bypass access controls, or exploit exposed systems. If you discover sensitive data, do not download, reuse, or disclose it; report it responsibly to the owner.
---
1. What Is Google Dorking?
Google dorking, also called Google hacking, is the use of search operators and carefully designed queries to locate specific information indexed by Google.
It does not break into Google or bypass authentication. It uses information that Google has already indexed.
Common goals include:
Finding public documentation
Locating academic papers and reports
Performing OSINT research
Auditing your own website's indexed content
Identifying accidentally indexed files
Discovering outdated pages
Troubleshooting search visibility
Finding public technology and security documentation
Monitoring changes to an organization's public web presence
Basic query
```text
site:example.com security policy
```
This searches for pages related to `security policy` on `example.com`.
---
2. Important 2026 Reality Check
Google does not guarantee that every historical operator will continue to work.
Operator behavior depends on:
Google Search updates
Indexing and ranking changes
Query context
Country and language
Search vertical, such as Web, Images, News, or Books
Personalization and SafeSearch
Whether the target content is indexed
Query complexity and automated abuse controls
Google's official documentation explicitly documents operators such as `site:`, `filetype:`, `imagesize:`, and `src:`. Other commonly used operators may work in practice but should be treated as variable or undocumented, not guaranteed.
Rule: Always test a query against a harmless, known example and verify the result manually.
---
3. Query Fundamentals
3.1 Normal keywords
Description
Searches for a topic using ordinary words.
Syntax
```text
keyword1 keyword2 keyword3
```
Example
```text
network intrusion detection
```
Use
Useful when you do not know the exact wording or location of the information.
---
3.2 Exact phrase: `"..."`
Description
Searches for an exact phrase or close exact wording.
Syntax
```text
"exact phrase"
```
Examples
```text
"incident response plan"
"zero trust architecture"
"security operations center"
```
Use
Finding repeated wording
Locating a known document title
Searching for a specific sentence
Reducing irrelevant results
Notes
Google may still apply some search interpretation. Exact matching is useful, but it is not a guarantee of literal byte-for-byte matching.
---
3.3 Exclusion: `-`
Description
Removes results containing a term.
Syntax
```text
keyword -excluded_term
```
Examples
```text
python security -jobs
cloud security -course
jaguar speed -car
```
Important rule
Do not insert a space between `-` and the excluded term.
Correct:
```text
security -jobs
```
Usually ineffective:
```text
security - jobs
```
---
3.4 OR
Description
Searches for either of multiple alternatives.
Syntax
```text
term1 OR term2
```
Examples
```text
"incident response" OR "digital forensics"
SOC OR SIEM
```
Notes
Use uppercase `OR` for clarity.
---
3.5 Grouping: `( )`
Description
Groups alternatives or complex search logic.
Syntax
```text
(group1 OR group2) additional_term
```
Examples
```text
("SOC analyst" OR "security analyst") internship
(site:example.com OR site:example.org) cybersecurity
```
Use
Grouping makes complex queries easier to understand and maintain.
---
3.6 Wildcard: `*`
Description
Acts as a placeholder in some phrase-search situations.
Syntax
```text
"word * word"
```
Example
```text
"best * for cybersecurity"
```
Notes
Wildcard behavior is context-dependent. Do not assume it behaves like a general regular-expression engine.
---
3.7 Number ranges: `..`
Description
Can be used to search for a numeric range in suitable queries.
Syntax
```text
keyword number1..number2
```
Example
```text
laptop cybersecurity 50000..80000
```
Notes
Range interpretation is not universal. Google may interpret the numbers as ordinary terms depending on the query.
---
4. Domain and Website Operators
4.1 `site:`
Description
Restricts results to a domain, subdomain, URL prefix, or top-level domain.
Syntax
```text
site:domain.example keyword
```
Examples
```text
site:example.com privacy policy
site:docs.example.com API
site:.edu cybersecurity research
site:.gov incident response
site:example.com filetype:pdf
```
Defensive uses
Review your own indexed pages
Locate old policy documents
Audit public documentation
Find pages that should be removed from indexing
Notes
Do not add a space after the colon.
Correct:
```text
site:example.com
```
Incorrect:
```text
site: example.com
```
---
4.2 Search a subdomain
Description
Restricts results to a specific subdomain.
Syntax
```text
site:subdomain.example.com keyword
```
Example
```text
site:docs.example.com authentication
```
Use
Useful for documentation, support portals, blogs, and knowledge bases.
---
4.3 Search a URL prefix
Description
Restricts results to a URL prefix in supported contexts.
Syntax
```text
site:https://example.com/path/ keyword
```
Example
```text
site:https://example.com/blog/ cybersecurity
```
Notes
Results may not exactly correspond to every URL under the prefix. Use the result URLs for manual verification.
---
4.4 Search a top-level domain
Description
Searches domains using a top-level domain or domain category.
Syntax
```text
site:.tld keyword
```
Examples
```text
site:.org digital forensics
site:.edu network security
site:.gov cyber safety
```
Use
Helpful for academic, government, nonprofit, or regional research.
---
4.5 Combine multiple domains
Syntax
```text
(site:example.com OR site:example.org) keyword
```
Example
```text
(site:owasp.org OR site:nist.gov) authentication
```
---
5. File and Document Operators
5.1 `filetype:`
Description
Restricts results to a file type or content type recognized by Google.
Syntax
```text
filetype:extension keyword
```
Examples
```text
filetype:pdf network security
filetype:pptx incident response
filetype:xlsx risk assessment
filetype:docx security policy
filetype:txt research notes
```
Common extensions
```text
pdf
doc
docx
xls
xlsx
ppt
pptx
txt
csv
rtf
xml
json
html
```
Defensive use
Audit your own website for documents that should be public, restricted, updated, or removed.
---
5.2 `ext:`
Description
Commonly used as an alternative to `filetype:` in practical search workflows.
Syntax
```text
ext:pdf keyword
```
Example
```text
site:example.com ext:pdf annual report
```
Reliability
Treat `ext:` as less formally documented than Google's core documented operators. If it behaves unexpectedly, use `filetype:` instead.
---
5.3 Search multiple file types
Syntax
```text
(site:example.com) (filetype:pdf OR filetype:docx) policy
```
Example
```text
site:example.com (filetype:pdf OR filetype:pptx) security
```
---
5.4 Exclude file types
Syntax
```text
site:example.com documentation -filetype:pdf
```
Notes
Operator combinations can be inconsistent. Validate results manually.
---
6. Page Location Operators
These operators are widely used in practical SEO and OSINT workflows, but Google does not promise that every undocumented operator will remain stable.
6.1 `intitle:`
Description
Looks for a word or phrase in the page title.
Syntax
```text
intitle:keyword
```
Examples
```text
intitle:"incident response"
intitle:documentation API
intitle:research cybersecurity
```
Use
Finding pages with a known title term
Locating documentation
Searching research resources
Discovering public pages with specific headings
---
6.2 `allintitle:`
Description
Requests that following terms appear in the title.
Syntax
```text
allintitle:term1 term2 term3
```
Example
```text
allintitle:network security monitoring
```
Caution
`allintitle:` can interact unexpectedly with later terms. Prefer multiple `intitle:` operators when you need predictable composition.
---
6.3 `inurl:`
Description
Looks for a term in the URL.
Syntax
```text
inurl:keyword
```
Examples
```text
inurl:docs API
inurl:blog cybersecurity
inurl:research threat detection
```
Use
Finding documentation sections
Locating blog categories
Searching URL naming patterns
Reviewing public site structure
---
6.4 `allinurl:`
Description
Requests that following terms appear in the URL.
Syntax
```text
allinurl:term1 term2
```
Example
```text
allinurl:security policy
```
Caution
Treat this operator as variable. `inurl:` is often easier to combine with other terms.
---
6.5 `intext:`
Description
Looks for a term in the text of a page.
Syntax
```text
intext:keyword
```
Examples
```text
intext:"responsible disclosure"
intext:"security policy" site:example.com
```
Use
Finding pages containing a particular phrase
Locating public policy statements
Searching for a known technical term
---
6.6 `allintext:`
Description
Requests that following terms appear in page text.
Syntax
```text
allintext:term1 term2
```
Example
```text
allintext:incident response playbook
```
Caution
Use with care in complex queries because all-in operators may consume the terms that follow them.
---
7. Date Operators
7.1 `before:`
Description
Finds results associated with dates before a specified date.
Syntax
```text
before:YYYY-MM-DD keyword
```
Examples
```text
before:2025-01-01 cybersecurity policy
before:2024/01/01 "incident response"
```
---
7.2 `after:`
Description
Finds results associated with dates after a specified date.
Syntax
```text
after:YYYY-MM-DD keyword
```
Example
```text
after:2026-01-01 cloud security
```
---
7.3 Combine `before:` and `after:`
Syntax
```text
after:YYYY-MM-DD before:YYYY-MM-DD keyword
```
Example
```text
after:2025-01-01 before:2026-01-01 zero trust
```
Important limitation
Date operators may reflect Google's interpretation of publication or update dates. They are not a perfect historical database filter.
---
8. Image Search Operators
These operators are primarily intended for Google Images.
8.1 `imagesize:`
Description
Searches for images with a specified pixel dimension.
Syntax
```text
imagesize:WIDTHxHEIGHT
```
Example
```text
imagesize:1920x1080 cybersecurity
```
Use
Finding images with a particular resolution
Locating diagrams or wallpapers
Researching image dimensions
---
8.2 `src:`
Description
Finds pages that reference a specific image URL in an image source attribute.
Syntax
```text
src:https://example.com/path/image.png
```
Example
```text
src:https://example.com/images/logo.png
```
Notes
This is an image-search operator. It is not a general web crawler and does not guarantee exhaustive discovery.
---
8.3 Image-search workflow
Open Google Images.
Start with a descriptive keyword.
Add `site:` if you want a specific domain.
Add `imagesize:` when resolution matters.
Check licensing and usage rights before reusing an image.
Verify the original source instead of trusting a repost.
---
9. News and Source-Oriented Searching
9.1 `source:`
Description
Commonly used in Google News to restrict results to a publication or source.
Syntax
```text
source:publication keyword
```
Example
```text
source:reuters cybersecurity
```
Caution
This operator is primarily relevant to Google News and may not behave the same way in ordinary Web Search.
---
9.2 News research pattern
Syntax
```text
("incident response" OR "data breach") after:2026-01-01 source:reuters
```
Good practice
Verify the date
Read the original report
Separate confirmed facts from claims
Check multiple reliable sources
Avoid treating snippets as complete evidence
---
10. Definition and Reference Searches
10.1 `define:`
Description
Requests a definition for a term.
Syntax
```text
define:term
```
Examples
```text
define:OSINT
define:phishing
define:telemetry
```
Use
Useful for quickly checking terminology, but consult authoritative documentation for technical or legal definitions.
---
11. Advanced Query Construction
11.1 Layered query design
A reliable advanced query usually contains:
Scope — where to search
Topic — what to search
Format — what kind of result
Time — when it was published or updated
Exclusions — what to remove
Template
```text
site:DOMAIN TOPIC filetype:TYPE after:DATE -EXCLUDED_TERM
```
Example
```text
site:nist.gov incident response filetype:pdf after:2024-01-01 -draft
```
---
11.2 Progressive narrowing
Start broad:
```text
cloud security
```
Add a domain:
```text
site:example.com cloud security
```
Add a format:
```text
site:example.com cloud security filetype:pdf
```
Add an exact phrase:
```text
site:example.com "cloud security architecture" filetype:pdf
```
Add a date range:
```text
site:example.com "cloud security architecture" filetype:pdf after:2024-01-01
```
Why this works
It helps you understand which part of the query removes useful results. Overly complex queries can hide relevant content.
---
11.3 Alternative-term expansion
Syntax
```text
(term1 OR term2 OR term3) subject
```
Example
```text
("security operations center" OR SOC OR "incident response") training
```
Use
Useful when organizations use different names for the same concept.
---
11.4 Domain plus title plus format
Syntax
```text
site:DOMAIN intitle:TERM filetype:TYPE
```
Example
```text
site:example.com intitle:documentation filetype:pdf
```
---
11.5 Domain plus URL term plus exact phrase
Syntax
```text
site:DOMAIN inurl:PATH "EXACT PHRASE"
```
Example
```text
site:example.com inurl:docs "API authentication"
```
---
11.6 Multiple exclusions
Syntax
```text
topic -term1 -term2 -term3
```
Example
```text
python cybersecurity -jobs -salary -course
```
Caution
Do not exclude too many terms too early. You may remove relevant results.
---
11.7 Search for public policy material
Syntax
```text
site:DOMAIN ("privacy policy" OR "security policy" OR "acceptable use")
```
Example
```text
site:example.org ("privacy policy" OR "security policy")
```
---
11.8 Search academic material
Syntax
```text
(site:.edu OR site:arxiv.org OR site:scholar.google.com) TOPIC
```
Example
```text
(site:.edu OR site:arxiv.org) intrusion detection machine learning
```
Notes
Google Scholar is a separate search service and has its own ranking and search behavior.
---
11.9 Search public standards
Syntax
```text
(site:nist.gov OR site:iso.org OR site:owasp.org) TOPIC
```
Example
```text
(site:nist.gov OR site:owasp.org) secure authentication
```
---
12. Defensive Website Exposure Assessment
Only perform these checks on domains and assets you own or have explicit permission to assess.
12.1 Establish scope
Document:
Authorized domain names
Subdomains included
Date of authorization
Contact person
Permitted actions
Prohibited actions
Reporting method
---
12.2 Review indexed pages
```text
site:yourdomain.example
```
Record:
Unexpected pages
Old pages
Duplicate pages
Development documentation
Unwanted cached descriptions
Pages containing outdated branding
---
12.3 Review indexed document types
```text
site:yourdomain.example (filetype:pdf OR filetype:docx OR filetype:xlsx)
```
Check whether each document:
Is intended to be public
Contains outdated information
Contains personal data
Contains internal metadata
Has correct access controls
Should be removed from indexing
Do not attempt to access a document that is not intended for you.
---
12.4 Review public development references
Safe example:
```text
site:yourdomain.example (inurl:docs OR inurl:blog OR inurl:help) developer
```
Look for:
Public API documentation
Versioning information
Deprecated pages
Public changelogs
Security contact details
Do not use search results as permission to test, log in, exploit, or bypass controls.
---
12.5 Review old content
```text
site:yourdomain.example after:2020-01-01 before:2024-01-01
```
Use this to identify potentially outdated content for a content-governance review.
---
12.6 Report an exposure
A responsible report should include:
Affected URL
Date and time discovered
Why the information may be sensitive
Minimal evidence
No unnecessary downloaded copies
Recommended remediation
Your contact details
A request for confirmation
---
13. Cybersecurity OSINT Workflows
13.1 Threat-intelligence research
Use public and authorized sources to research a topic.
```text
("threat actor" OR campaign OR malware) "industry name" after:2025-01-01
```
Useful additions:
```text
filetype:pdf
site:vendor.example
"technical report"
"indicator of compromise"
```
Verification checklist
Is the source credible?
Is the publication date clear?
Is the claim confirmed or speculative?
Is the information current?
Can it be cross-checked with another source?
Is the indicator still relevant?
---
13.2 Vulnerability research
Use searches for public advisories and defensive documentation rather than searching for exposed targets.
```text
site:nvd.nist.gov "CVE-YYYY-NNNNN"
```
```text
site:vendor.example security advisory "CVE-YYYY-NNNNN"
```
```text
"CVE-YYYY-NNNNN" mitigation
```
Avoid using search queries to locate unauthorized systems, credentials, private keys, or administrative interfaces.
---
13.3 Security documentation research
```text
("hardening guide" OR "secure configuration") operating system filetype:pdf
```
```text
site:cisecurity.org hardening guide
```
```text
site:owasp.org authentication cheat sheet
```
---
13.4 Incident-response research
```text
("incident response playbook" OR "incident handling guide") filetype:pdf
```
```text
site:nist.gov incident response guide
```
```text
("digital forensics" OR "memory forensics") "best practices"
```
---
14. Search Reliability and Operator Status
14.1 More dependable operators
These are commonly documented or broadly supported:
Operator	Main purpose
`"phrase"`	Exact phrase searching
`-term`	Exclusion
`OR`	Alternatives
`site:`	Domain or URL scope
`filetype:`	File type
`before:`	Date boundary
`after:`	Date boundary
`imagesize:`	Image dimensions
`src:`	Image source reference
14.2 Operators that require testing
These are frequently used in practical search workflows but may be undocumented, context-dependent, or less stable:
Operator	Typical purpose
`intitle:`	Term in title
`allintitle:`	Multiple title terms
`inurl:`	Term in URL
`allinurl:`	Multiple URL terms
`intext:`	Term in body text
`allintext:`	Multiple body terms
`ext:`	File extension alias
`define:`	Definition lookup
`source:`	News source filtering
`*`	Wildcard-like phrase behavior
`..`	Numeric range behavior
Operational rule: Never build an important conclusion from one operator or one result snippet.
---
15. Common Mistakes
Mistake 1: Adding a space after an operator
Incorrect:
```text
site: example.com
```
Correct:
```text
site:example.com
```
---
Mistake 2: Assuming Google indexes everything
Google does not index every page, file, or URL.
Possible reasons:
`robots.txt`
`noindex`
Authentication
Crawl restrictions
Duplicate-content handling
Search quality systems
Temporary indexing changes
The content was never discovered
---
Mistake 3: Treating snippets as proof
A snippet can be:
Truncated
Outdated
Taken out of context
Generated from page content
Different from the current page
Always open the source and verify the information.
---
Mistake 4: Overusing all-in operators
Queries such as `allintext:` and `allintitle:` can make complex searches harder to control.
Use smaller queries first.
---
Mistake 5: Making assumptions from absence
If a query returns no result, it does not prove that the information does not exist.
It may be:
Not indexed
Blocked from crawling
Written differently
On another domain
Removed from search results
Outside the query's interpretation
---
Mistake 6: Using one source
For OSINT and threat intelligence, cross-check with:
Official advisories
Vendor documentation
Government sources
Academic research
Reputable reporting
Original publications
---
16. Practical Query-Building Framework
Use the following five-question framework:
Question 1 — What is my scope?
Examples:
```text
site:example.com
site:.edu
site:nist.gov
```
Question 2 — What exact information do I need?
Examples:
```text
"incident response"
"API authentication"
"privacy policy"
```
Question 3 — Where should the term appear?
Examples:
```text
intitle:documentation
inurl:docs
intext:"responsible disclosure"
```
Question 4 — What format do I want?
Examples:
```text
filetype:pdf
filetype:pptx
filetype:csv
```
Question 5 — What should be excluded?
Examples:
```text
-jobs
-draft
-advertisement
```
Full example
```text
site:example.com intitle:documentation "API authentication" filetype:pdf -draft
```
---
17. Query Testing Method
For each query:
Run the simplest version.
Note the approximate result quality.
Add one operator.
Compare the results.
Remove operators that hide useful results.
Open several results manually.
Record the source, date, and relevance.
Repeat with alternative terms.
Example progression
```text
network security
```
```text
"network security"
```
```text
site:nist.gov "network security"
```
```text
site:nist.gov "network security" filetype:pdf
```
```text
site:nist.gov "network security" filetype:pdf after:2024-01-01
```
---
18. Safe Practice Exercises
Use public educational domains, your own website, or a local documentation project.
Exercise 1 — Domain restriction
Goal: Find cybersecurity material from one domain.
```text
site:owasp.org cybersecurity
```
Questions:
Did all results come from the selected domain?
Which page types appeared?
What keywords could improve precision?
---
Exercise 2 — Exact phrase
Goal: Find a specific phrase.
```text
"incident response plan"
```
Questions:
How many results use the exact phrase?
Which results are official?
Which results are educational?
---
Exercise 3 — File type
Goal: Find public PDF resources.
```text
filetype:pdf "digital forensics"
```
Questions:
Are the PDFs relevant?
Are they current?
Are they from trustworthy sources?
---
Exercise 4 — Date filtering
Goal: Narrow research to a time period.
```text
after:2025-01-01 before:2026-01-01 "cloud security"
```
Questions:
Do the dates match the source's actual publication date?
Are there older documents appearing?
Does changing the date format affect results?
---
Exercise 5 — Defensive self-audit
Goal: Review your own domain.
```text
site:YOUR_DOMAIN
```
Then:
```text
site:YOUR_DOMAIN filetype:pdf
```
Then:
```text
site:YOUR_DOMAIN (inurl:docs OR inurl:help OR inurl:blog)
```
Document only information you are authorized to review.
---
19. Quick Reference Cheat Sheet
Syntax	Meaning	Example
`"..."`	Exact phrase	`"security policy"`
`-term`	Exclude term	`security -jobs`
`OR`	Alternative terms	`SOC OR SIEM`
`( )`	Group terms	`(SOC OR SIEM) training`
`site:`	Domain scope	`site:example.com`
`filetype:`	File format	`filetype:pdf`
`ext:`	File extension alias	`ext:pdf`
`intitle:`	Term in title	`intitle:documentation`
`allintitle:`	Multiple title terms	`allintitle:security policy`
`inurl:`	Term in URL	`inurl:docs`
`allinurl:`	Multiple URL terms	`allinurl:security policy`
`intext:`	Term in body	`intext:"responsible disclosure"`
`allintext:`	Multiple body terms	`allintext:incident response`
`before:`	Before a date	`before:2026-01-01`
`after:`	After a date	`after:2025-01-01`
`imagesize:`	Image dimensions	`imagesize:1920x1080`
`src:`	Image source URL	`src:https://example.com/a.png`
`source:`	News source context	`source:reuters`
`define:`	Definition lookup	`define:OSINT`
`*`	Wildcard-like phrase behavior	`"best * tool"`
`..`	Numeric range behavior	`price 100..500`
---
20. Recommended Operational Checklist
Before searching:
[ ] Define the purpose.
[ ] Confirm authorization.
[ ] Identify the scope.
[ ] Avoid personal or sensitive targeting.
[ ] Start with a simple query.
During searching:
[ ] Add one operator at a time.
[ ] Verify source URLs.
[ ] Check dates.
[ ] Cross-check important claims.
[ ] Avoid downloading unnecessary sensitive material.
[ ] Do not attempt unauthorized access.
After searching:
[ ] Record the query and date.
[ ] Record relevant URLs.
[ ] Preserve only necessary evidence.
[ ] Remove sensitive data from notes.
[ ] Report accidental exposure responsibly.
[ ] Re-test after remediation.
---
21. Final Notes
Google dorking is best understood as precision search, not as a guaranteed vulnerability-discovery system.
The most valuable skills are:
Understanding the target and scope
Choosing the right keywords
Applying operators carefully
Verifying results manually
Understanding indexing limitations
Maintaining legal and ethical boundaries
Documenting findings clearly
Use Google search operators as one part of a larger OSINT and defensive-security workflow. For technical security testing, use authorized scanners, asset inventories, log analysis, vulnerability databases, and dedicated assessment tools instead of relying on search results alone.
Official references
Google Search Help — Refine Google searches:
https://support.google.com/websearch/answer/2466433
Google Advanced Search:
https://www.google.com/advanced_search
Google Search Central — Search operators:
https://developers.google.com/search/docs/monitor-debug/search-operators
