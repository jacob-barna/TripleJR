## CYBR 8420 - Assurance Cases for Software Security Engineering

**Github Repository: https://github.com/jacob-barna/TripleJR**

**Authors:** Jeffrey Smith, Ronald Ramirez, Jacob Barna, Jill Lenz

**Team Name:** TripleJR

## Instructions
### A markdown report that includes the following:

Using security requirements, identify five assurance claims
Prepare a convincing argument in support of the claims. Document this argument using an assurance case for each of the claims.
Assess the alignment of the planned evidence with that available (or can be made available) from the OSS project. Highlight the gaps.
Link to your team GitHub repository that shows your internal project task assignments and collaborations to finish this task. Also, include a summary of your team reflection meeting. What issues occurred? What did you plan to change moving forward? 
Only one submission per team.

More details: https://robinagandhi.github.io/swa/slides/lecture-2/assurance-case-exercise.html

### Assurance Claim 1 - Shields component prevents unauthorized tracking.
![Assurance Claims - Browsing](https://user-images.githubusercontent.com/25576618/66617138-70698d00-eb99-11e9-887a-4339726b8dbf.png)

#### Evidence For Claim 1

*Inside my Word Doc and will post into Git*

### Assurance Claim 2 - The browser provides adequate confidentiality of communications.
![Assurance Claims - HTTPS](https://user-images.githubusercontent.com/31263469/66679878-dfe08a80-ec34-11e9-8fd2-c954f9849a68.png)

Evidence: 

Bug Bounty Reports
Brave participates in a bug bounty program through HackerOne.  According to HackerOne, there have been 123 reports resolved and $30,515 paid in bounties, and Brave responds to reports within 22 hours on average [1].

Unit Tests
Brave has a suite of unit tests and browser tests that must be run for each pull request [2].  The test results are not publicly available without running the project locally, although the Brave team hopes to make the results public in the future [2].

Open Source Code Review by Third Parties
There are known experts not employed by Brave who are sometimes listed as contributors to issues.  For instance, Tavis Ormandy, a computer security expert employed by Google Project Zero has been named in issue reports [3].  There appears to be no evidence that Brave hires any known third party code auditors, which may constitute a gap in evidence needed.  Brave falls back on the claim that "if anyone wanted to audit us, they're more than welcome to." [4]

Issue Tracker
There is an issue tracker for each of the Brave projects.  As of writing, there are 1,688 issues in the brave-browser github repo [5].  The word "security" appears in the body or tags of 81 of these open issues.  In addition, there are 176 such closed issues.  Drilling further into this vein of inquiry, there are 5 open and closed issues related to TLS.  So while there is an issue tracker present, there may be a gap in the claim that the browser can support secure communications.


Common Vulnerability and Exposure List 
As of this writing, there are only 4 issues in the Common Vulnerabilities and Exposures (CVE) database [6].  All of the entries relate to prior versions of the browser.  This evidence seems to support the claim that the encryption used by Brave is not exploitable. 

Malware Test Reports 
There don't appear to be any malware test results available at the time of this writing.  The closest thing found are articles mentioning that "Brave comes with Google Safe Browsing, which scans the URLs you visit for potential malware." [7]  Since Brave is also based on Chromium, it comes with built-in protection from malware performing Man-in-the-Middle attacks, provided the malware causes SSL errors.  Despite having claims against malware, the test results remain to be seen, signalling a potential gap in the evidence.


Test Results 
Test results are not publicly available without running the code locally.  As of writing, the unit tests have not been run locally to determine the amount of code coverage.  However, this will be done in future research to identify if code coverage is unacceptable.  Since the Brave browser is based on Chromium, it seems unlikely that any gaps will be uncovered here.

Expert Profiles
Brave employees Yan Zhu, a widely known expert on cryptography, as Chief Security Officer [8].  Using a recently closed pull request related to security, it is noted that a Brave software employee "ryanml" approved the changes [9].  The only indication that this user is an expert is the fact that they are employed by Brave, and perhaps that there are 63 people following this individual.  

Pull Request Reviews 
There is a policy that each pull request be approved by reviewers who are employees [10].  As mentioned, the expertise of the employees is somewhat murky, but that probably does not constitute an evidence gap as they are employed as software engineers for a company led by known experts.

Cybersecurity Expert Test Reports
There may be a gap in the evidence on whether TLS is safe or not.  Brave, because it uses BoringSSL is relatively safe when TLS 1.3 is enabled; TLS 1.3 has been recently shown to be vulnerable to a downgrade attack allowing observation of encrypted messages and more [11].  However, it is not using the downgrade protections present in TLS 1.3 for all connections to allow vendors to fix proxy software [12].  In addition, Brave, being based on Chromium, displays warning messages for TLS 1.0 and 1.1 [12], but TLS 1.2 has no such warning despite being the target of several recent and successful attacks [13].  More research needs to be done in this area to identify if Brave is indeed properly implementing TLS 1.2 and whether or not Brave is subject to attacks when communicating with the proxy software that is not protected by TLS 1.3 downgrade protection. 


### Assurance Claim 3 - The built-in password manager prevents unauthorized access to data. 
### Assurance Claim 4 - The browser wallet sufficiently secures reward contributions.   

- second draft on image (need to reference other claims)

![Assurance Claims - Wallet -  (3)](https://user-images.githubusercontent.com/45551925/66665790-df37fc00-ec14-11e9-9b96-1be3c94a2d99.png)



#### Evidence 

As you can see, this claim states that the systems wallet rewards program will give the user full control over their ability to contribute to authors. It is important to note that the Brave wallet rewards program allows the user to help fund the content they love even when the browser is blocking advertisements. The Brave browser has a built in wallet that allows user to individually fund their account so they can support their favorite creators or simply get rewarded with Basic Attention Token (BATs). BAT’s are divided up based on the users attention, based on the sites they have visited. All of this is done anonymously, giving the user privacy and the ability to have full control over which creators they would like to support. 

more info to come ....

### Assurance Claim 5 - The browser minimizes malicious third-party extension.  

*https://support.brave.com/hc/en-us/articles/360017909112-How-can-I-add-extensions-to-Brave-*



![image](https://user-images.githubusercontent.com/45551925/66178974-cf288700-e62c-11e9-9955-7fa63e48c7a7.png)


### Summary of team reflection
As a team, we have collectively agreed that even though we have successfully completed all the project requirements as of now, we have had some ups and downs. We use Lucid chart for our diagrams, Discord and GitHub, and class time for our communication and collaboration. During the development of our proposal and use/misuse case development, GitHub collaboration was not used to the full potential or was slow to start. However, for the assurance assignment, there was better collaboration on GitHub and better use of the features. The slow start was due to all the communication via Discord. Collaboration from other sources could be moved from applications such as Discord and integrated into GitHub to track communication and collaboration better. During the assurance assignment, the creation of claims and rebuttals were underestimated and led to problems coming up with broad claims. However, after getting started with a strong initial claim, the team was able to develop the remaining claims with less trouble. The initial thought that claims had to be proved "true" turned out to be false, and with evidence, the claims could be proved "false" or not secure. We also will be using the professor's suggestions he mentioned, by utilizing the Github issue board to make comments on issues we are working on. This helps our team stay organized. Regarding the individual contributions, we are in an agreeance that everyone has been open to receiving responsibilities and successful at meeting the deadlines.

## Team GitHub 
[Team Repo](https://github.com/jacob-barna/TripleJR)  
[Team Project Board](https://github.com/jacob-barna/TripleJR/projects/3)  

[1]: https://hackerone.com/brave
[2]: https://github.com/brave/brave-browser/wiki/PR-Builder-overview
[3]: https://github.com/brave/browser-laptop/issues/4753
[4]: https://www.reddit.com/r/brave_browser/comments/9t85hf/does_brave_plan_to_undergo_a_formal_independent/
[5]: https://github.com/brave/brave-browser/issues
[6]: https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=brave+browser
[7]: https://www.cloudwards.net/brave-review/
[8]: https://brave.com/ama-with-yan-zhu/
[9]: https://github.com/brave/ethereum-remote-client/pull/62
[10]: https://github.com/brave/browser-laptop/blob/master/CONTRIBUTING.md#employees-should
[11]: https://www.nccgroup.trust/us/about-us/newsroom-and-events/blog/2019/february/downgrade-attack-on-tls-1.3-and-vulnerabilities-in-major-tls-libraries/
[12]: https://www.ghacks.net/2019/10/02/tls-1-0-and-1-1-deprecation-chrome-to-display-your-connection-is-not-fully-secure-warnings/
[13]: https://acunetix.com/blog/articles/tls-vulnerabilities-attacks-final-part/
