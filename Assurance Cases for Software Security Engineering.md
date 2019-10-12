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
![Assurance Claims - Browsing](https://user-images.githubusercontent.com/25576618/66690060-51c7cc80-ec53-11e9-92a3-4ef1747b7460.png)

### Evidence:

#### E1: Shields site specific setting
Out of the box Brave Shields security features are enabled by default. This ensures privacy basics are enabled to protect privacy, however for certain sites additional restrictions are needed for protection. To provide this additional security, Shields allows the user to secure configure site-specific settings. This setting is persistent and will not change even if global settings are modified [15].

#### E2: Ads and cross-site trackers setting
When browsing websites there is always the possibility that ads, for revenue or malicious purposes, are inserted into the site. In addition to be a nuisance and causing a bad user experience there is a security risk behind the scenes. These ads can come with trackers that allow the entity that embedded them to retrieve data about the sites and actions taken while browsing. By default, Shields blocks the majority of these ads and the trackers that come with them [16]. Additionally, additions have been made to the code to provide better protection and identification of the ads through stronger rules and algorithms [17].

#### E3: Cross-site cookies setting
In addition to ads websites also can also implement cross-site cookies to track user activates and settings as well. In some cases, the user wants cross-site, aka third-party, cookies to be enabled to maintain site functionality of sites. However, these cross-site cookies have the ability to maintain persistence from site to site and report the activities is logs. Shields combats this by using strictly blocking these cookies by default and allowing further restrictions based on user preferences [16] [18].

#### E4: Cross-site device recognition setting
While browsing the internet there is the possibility that sites or third-parties will try to identify, or fingerprint, the device being used. This information poses a security risk as it reveals specifics about the user’s device that can be mis-used for malicious purposes. These fingerprinting technologies can be stopped when using Brave [19]. By default, Shields blocks these actions and can be modified as well by the user [16].

#### E5: HTTPS connection upgrading setting
By default, Shields automatically will securely upgrade the user’s connections to sites [16]. In doing so the connection will be changed from HTTP to HTTPS. This ensures the traffic is being encrypted and security resulting in the user’s privacy being maintained.

#### E6: Malicious code and sites setting
By default, Shields will block malicious code and malicious sites. Some examples of this would be code that will try to use your computer to mine cryptocurrencies [16].

#### E7: Cookie disablement setting
As discussed in E3, cross-site cookies are disabled by default, but first-party cookies remain active. This allows for the use of functions such as shopping carts or login persistence which could assist the user. However, some malicious sites can implement cross-site cookies as first-party cookies. To prevent this globally across Brave, or site-specifically, Shields allows for the configuration and fine tuning of cookies including the disablement of all cookies [20].

#### E8: JavaScript prevention setting
As discussed in E6, malicious code and sites are blocked by default, but scripts are allowed to run inside Brave. This poses a threat of not only allowing malicious actions to occur but could allow for the use of cross-site tracking inside the code. If needed, the user can block JavaScript and others scripts by enabling the feature through Shields [20].

### Assurance Claim 2 - The browser provides adequate confidentiality of communications.
![Assurance Claims - HTTPS](https://user-images.githubusercontent.com/25576618/66690083-6dcb6e00-ec53-11e9-9bcf-468d8ba389ac.png)

### Evidence: 

#### E1: Bug Bounty Reports
Brave participates in a bug bounty program through HackerOne.  According to HackerOne, there have been 123 reports resolved and $30,515 paid in bounties, and Brave responds to reports within 22 hours on average [1].

#### E2: Unit Tests
Brave has a suite of unit tests and browser tests that must be run for each pull request [2].  The test results are not publicly available without running the project locally, although the Brave team hopes to make the results public in the future [2].

#### E3: Open Source Code Review by Third Parties
There are known experts not employed by Brave who are sometimes listed as contributors to issues.  For instance, Tavis Ormandy, a computer security expert employed by Google Project Zero has been named in issue reports [3].  There appears to be no evidence that Brave hires any known third party code auditors, which may constitute a gap in evidence needed.  Brave falls back on the claim that "if anyone wanted to audit us, they're more than welcome to." [4]

#### E4: Issue Tracker
There is an issue tracker for each of the Brave projects.  As of writing, there are 1,688 issues in the brave-browser github repo [5].  The word "security" appears in the body or tags of 81 of these open issues.  In addition, there are 176 such closed issues.  Drilling further into this vein of inquiry, there are 5 open and closed issues related to TLS.  So while there is an issue tracker present, there may be a gap in the claim that the browser can support secure communications.

#### E5: Common Vulnerability and Exposure List 
As of this writing, there are only 4 issues in the Common Vulnerabilities and Exposures (CVE) database [6].  All of the entries relate to prior versions of the browser.  This evidence seems to support the claim that the encryption used by Brave is not exploitable. 

#### E6: Malware Test Reports 
There don't appear to be any malware test results available at the time of this writing.  The closest thing found are articles mentioning that "Brave comes with Google Safe Browsing, which scans the URLs you visit for potential malware." [7]  Since Brave is also based on Chromium, it comes with built-in protection from malware performing Man-in-the-Middle attacks, provided the malware causes SSL errors.  Despite having claims against malware, the test results remain to be seen, signalling a potential gap in the evidence.

#### E7: Test Results 
Test results are not publicly available without running the code locally.  As of writing, the unit tests have not been run locally to determine the amount of code coverage.  However, this will be done in future research to identify if code coverage is unacceptable.  Since the Brave browser is based on Chromium, it seems unlikely that any gaps will be uncovered here.

#### E8: Expert Profiles
Brave employees Yan Zhu, a widely known expert on cryptography, as Chief Security Officer [8].  Using a recently closed pull request related to security, it is noted that a Brave software employee "ryanml" approved the changes [9].  The only indication that this user is an expert is the fact that they are employed by Brave, and perhaps that there are 63 people following this individual.  

#### E9: Pull Request Reviews 
There is a policy that each pull request be approved by reviewers who are employees [10].  As mentioned, the expertise of the employees is somewhat murky, but that probably does not constitute an evidence gap as they are employed as software engineers for a company led by known experts.

#### E10: Cybersecurity Expert Test Reports
There may be a gap in the evidence on whether TLS is safe or not.  Brave, because it uses BoringSSL is relatively safe when TLS 1.3 is enabled; TLS 1.3 has been recently shown to be vulnerable to a downgrade attack allowing observation of encrypted messages and more [11].  However, it is not using the downgrade protections present in TLS 1.3 for all connections to allow vendors to fix proxy software [12].  In addition, Brave, being based on Chromium, displays warning messages for TLS 1.0 and 1.1 [13], but TLS 1.2 has no such warning despite being the target of several recent and successful attacks [14].  More research needs to be done in this area to identify if Brave is indeed properly implementing TLS 1.2 and whether or not Brave is subject to attacks when communicating with the proxy software that is not protected by TLS 1.3 downgrade protection. 

### Assurance Claim 3 - The built-in password manager prevents unauthorized access to data.

### Evidence:

#### E1: 

#### E2:

### Assurance Claim 4 - The browser wallet sufficiently secures reward contributions.   

![Assurance Claims - Wallet -  (4)](https://user-images.githubusercontent.com/45551925/66692261-44660e80-ec62-11e9-9ccd-5099c30cd1d5.png)

### Evidence:


#### E1: Assurance Case #2 E1 - 4, E7 - E9   
For the evidence supporting C5, mentioning how the browser implements HTTPS correctly, refuting the possibility of a man-in-the-middle attack in an attempt to steal login credentials and rewards is detailed in the Assurance Case #2 Evidence 1 - 4 and Evidence 7 - 9. 


#### E2: Brave Shields 

In support for E1, the Brave browser implements Shields which protects users user privacy as they browse the web. This means that out of the box, Shields protects ad blocking, discarding cookies other than the ones from sites actually visited, secure connection upgrading, and the blocking of malicious code and sites, like ones that will use the users computer to mine cryptocurrencies. However though, as the documentation states in E6, “Configuring your protections to the highest level by blocking JavaScript and all cookies will keep your browser safer, but it may also break some sites.” This is something that is not enabled out of the box which would improve security tremendously but is not enabled by default. [Link](https://support.brave.com/hc/en-us/articles/360022806212-How-do-I-use-Shields-while-browsing-
) Nevertheless, the default configuration still prevents cross-site trackers as shown in the [sample code](https://github.com/brave/tracking-protection/blob/master/README.md) below. 

```c++

    // Returns combined result of third party hosts for "google.com" and for "subdomain.google.com"
    // "facebook.fr,facebook.de,2mdn.net,admeld.com"
    char* thirdPartyHosts = parser.findFirstPartyHosts("subdomain.google.com");
    if (nullptr != thirdPartyHosts) {
        cout << thirdPartyHosts << endl;
        delete []thirdPartyHosts;
    }

```


#### E3: Malware Tests Reports
Not much information was found in regards to malware test reports. The one our group found as referenced in Assurance Claim #2: E6, is a review from [Cloudwars](https://www.cloudwards.net/brave-review/). This seems to be a gap that we noticed when finding evidence to support Claim C6. 

#### E4: Brave Build Channels

The [Brave Build Channels](https://brave.com/download-beta/) refers to the fast iterative development cycle that Brave goes through when releasing an update. They have 4 different version that follows:
Brave Nightly
Is the testing and developed version; releases are updated nightly and may contain bugs 
Brave Dev
Is an unpolished and unfinished version, showing the work in progress
Brave Beta
Early preview for new version of Brave, showcases new advancements coming soon
Brave Release
Official release version of the app

#### E5:  Manual Testing 
To verify, I conducted a manual test as shown in E5, to see if this was truly the case. I reset my settings due to the adjustments I made when testing out this browse and once my settings were reset, the “Block scripts” button was not checked. 

![braveShields_settings](https://user-images.githubusercontent.com/45551925/66692365-572d1300-ec63-11e9-9df1-179d6b9977d8.png)

Enabling this by default is something that could be looked at in order to provide maximum protection and security for users. Nevertheless, this was a gap in evidence needed to support C9.

#### E6: Shield Documentation

As discussed during E2, the [Brave Shields Documentation](https://support.brave.com/hc/en-us/articles/360022806212-How-do-I-use-Shields-while-browsing-
) states that script blocking is not on by default since sites may break, preventing a user to view their desired web page they are surfing to. This is a slight gap we noticed the evidence needed to support C9. The user would have to adjust this manually in order to successfully obtain the blocking of scripts despite further web experience issues. This could be something to review in order to obtain a more secure interaction when surfing the web. 


### Assurance Claim 5 - The browser minimizes malicious third-party extension.  
![Assurance Claims - 3rd Party Extension](https://user-images.githubusercontent.com/25576618/66690105-889de280-ec53-11e9-9c6d-63c1f9b4406b.png)

*https://support.brave.com/hc/en-us/articles/360017909112-How-can-I-add-extensions-to-Brave-*

### Evidence:

#### E3: Google SafeBrowsing
Brave allows the use of extensions that are published to the Chrome Web Store. This poses a security risk to the users of Brave as extensions in the Web Store could be malicious. After researching, no information was able to be located about the scanning of uploaded extensions. However, it was determined that Google conducts infrastructure scanning with SafeBrowsing actions which includes items in the Web Store [21]. This allows for a gap in security as malicious items can be uploaded to the store and may be present for an unknown amount of time until a user reports a threat or Google happens to come across the item in one of the scans.

#### E2: Chromium Blog
With Google Chrome or Chromium, being open source, any user can be a developer and upload their projects for others to download and install. This poses a threat to Brave users as a malicious user could upload content that would create security issues. To combat this threat and mitigate the possibility of malicious content being uploaded through rouge accounts Google has implement Two Factor Authentication (2FA) for all developer accounts [22]. While this would prevent compromised accounts from uploading malicious items, it does not prevent a legitimate rouge user from uploading whatever they want. This gap allows security risks to enter into the Brave environment and exploit the user’s privacy and security.

#### E3: Extension installation
Before any extension can be installed, Brave requires the user to except or deny the permissions required by the extension [23]. This security practice is good as it requires an approval prior to an extension being installed and ran. However, a user with little knowledge about permissions, and their capabilities, or permissions that may be exploited after installed could be potentially installed result in security risks.

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
[12]: https://www.chromium.org/Home/tls13
[13]: https://www.ghacks.net/2019/10/02/tls-1-0-and-1-1-deprecation-chrome-to-display-your-connection-is-not-fully-secure-warnings/
[14]: https://acunetix.com/blog/articles/tls-vulnerabilities-attacks-final-part/
[15]: https://support.brave.com/hc/en-us/articles/360023646212-How-do-I-configure-global-and-site-specific-Shields-settings-
[16]: https://support.brave.com/hc/en-us/articles/360022973471-What-is-Shields-
[17]: https://brave.com/improved-ad-blocker-performance/
[18]: https://www.cnet.com/how-to/this-is-the-browser-youll-want-if-you-care-about-online-privacy/
[19]: https://www.wired.com/story/privacy-browsers-duckduckgo-ghostery-brave/
[20]: https://support.brave.com/hc/en-us/articles/360022806212-How-do-I-use-Shields-while-browsing-
[21]: https://safebrowsing.google.com/
[22]: https://blog.chromium.org/2018/10/trustworthy-chrome-extensions-by-default.html
[23]: https://support.brave.com/hc/en-us/articles/360017909112-How-can-I-add-extensions-to-Brave-
