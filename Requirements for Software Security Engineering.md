## CYBR 8420 - Requirements for Software Security Engineering

**Github Repository: https://github.com/jacob-barna/TripleJR**

**Authors:** Jeffrey Smith, Ronald Ramirez, Jacob Barna, Jill Lenz

**Team Name:** TripleJR
 
- [Observation Review of OSS Project Documentation for Security-Related Configuration and Installation Issues](#observation-review-of-oss-project-documentation-for-security-related-configuration-and-installation-issues)

---------------------------------------------------------------------------------------------------------------------
A markdown report that describes the following:

- Identify five essential data flows (source-transformations-sink) through the software. Develop use-cases diagrams related to these data flows. 
    - Make sure you have a back story in your operational environment. Where is this system being used? What is its criticality? Who are the stakeholders?
    - Ideally, the dataflows need to be spread across different external interactors (humans or systems) of your software. Once different external interactors have been identified, the use cases can focus on the most sensitive features used by the external interactor.

- Derive security requirements for the use-cases using misuse case diagrams. Briefly describe the analysis in each misuse case diagram.
    - The misusers should be contextualized in your environment of operation and relevant to the dataflows identified above. Use names that help the reader understand their motives, resources, attack of choice, and the available access to the system to carry out their attack.
---------------------------------------------------------------------------------------------------------------------
 

## Backstory

Brave is an open-source web browser that secures users privacy while still providing a fast browsing experience. The Brave browser blocks all advertisements and tracking mechanisms sites implement to provide a “better” experience to the users using their site. In our hypothetical environment, our targeted users continue to be privacy-minded people who will use the browser in a home or work environment if permitted on desktop and mobile devices.  

These users are also considered our stakeholders. Users using the Brave browser want to browse the web without being tracked or have advertisements popup, all while having privacy in mind. The Brave browser also provides a built-in password manager and autofill capabilities to allow our stakeholders to securely manage their passwords for their desired applications. Stakeholders are also looking for automatic upgrades to HTTPS, whenever possible to encrypt the communication. The Brave browser will do its best to upgrade standard unencrypted HTTP communication line, to a secure HTTPS medium. These are all features that our privacy minded stakeholders’ value deeply and are looking for in a web browser in the digital age today. 

With that being said, the five essential data flows that we have analyzed for the Brave browser is the following:
- Brave Browser Search Use Case
- SSL Use Case
- Password Manager Use Case
- Wallet Use Case
- Third-Party Extensions Use Case

### Brave Browser Search Use Case

#### Use Case

Peter, the privacy-minded user, expects that when utilizing the default search engine defined inside the Brave broswer that his privacy is respected. Peter excepts that the searches and sites visted from the search engine results are not tracked by thrid-parties and contained only in the local cache of his personal device. Brave browser does not block first-party cookies by default to allow for better user experience while navigating through individual sites to maintain persistance of user activities such as logins and shopping carts. Peter understands that disabling all cookies could result in the loss of these user experiences but the enabling of cookies could led to the possiblity of being tracked by third-party cookies or servers.

#### Misuse Case

Billy, the hacker wants to utilize third-party cookies on the Brave browser to track the sites and items Peter looks at while browsing the search engine and web. Billy expects that he will be able to monitize off of Peter's browsing activities by selling it to venders. He also hopes that the data can be used to determine what Peter is interested in to utilize targeted items to lure Peter to malicious sites or downloads. To accomplish this, Billy has determined that he can carry his malicious plan out in three different ways. The first action Billy takes is by setting a third-party tracking cookie as a first-party cookie to prevent being blocked on the search engine and browser. This will bypass any default or user set settings that attempt to block third-party cookies by being stored on Peter's device as a first-party cookie. The second action Billy takes is by initializing the third-party tracking cookies inside JavaScript to render and appear as first-party cookies on the search engine and broswer. Since the JavaScript is being rendered and executed on the website domain that is currently being displayed, Billy can have his third-party cookie used inside the code and appear as a first-party cookie. The last action Billy can take is by using DNS aliasing to mask his third-party tracking servers as a first-party server. By doing this, when the third-party server is contacted, the DNS aliasing can spoof a first-party server resulting in Peter's device to think that Billy's server is a first-party server.

#### Security Requirements

In order to prevent the attacks listed above in the misuse cases, there are features and settings that Peter excepts to see inside the Brave browser. To prevent the threat of third-party cookies being inialized as first-party cookies, Brave has default settings that will block all cookies except the first-party cookies of the domain that is currently being viewed in the browser. However, there is always the potential that the third-party cookie is implemented inside JavaScript which would appear to be a first-party cookie since the code is being executed on the current domain. To prevent this, site or global settings can be set by Peter to block JavaScript from being executed inside the browser. Lastly, if a third-party cookie server attempts to spoof a first-party server, through DNS aliasing, Peter can resort to disabling both third and first-party cookies. In doing so, the blocking of first-party cookies would prevent all three of the misuse cases resulting in Peter receiving the privacy he expects from the Brave broswer.

#### Diagram

<img width="1092" alt="Screen Shot 2019-09-30 at 12 05 27 PM" src="https://user-images.githubusercontent.com/25576618/65900082-babd6380-e37a-11e9-980d-1a70ed0059e5.png">

### SSL Use Case

#### Use Case

Peter, the privacy-minded user, expects that when visiting sites using SSL, the network traffic moving back and forth between his browser and the destination server is strongly encrypted. Peter expects this because he often purchases items online using his credit card number and sends other confidential information in chat programs. If SSL breaks down, these expectations will not be met.

#### Misuse Case

Billy, the hacker wants to eavesdrop on the communications between Billy's browser and the sites he visits with SSL. Billy expects that he will find the information and he will be able to exploit for nefarious uses such as identity theft, credit card fraud, and blackmail. Billy can use several attacks at his disposal to attempt to monitor the communications. The ideal attack would be to create a Man-in-the-middle (MiTM) attack in which a certificate that he owns is used by Peter to encrypt traffic. This type of attack would compromise all of Peter's SSL communications as Billy would surreptitiously siphon unencrypted traffic as it flows past. If this attack doesn't work, there is a variation of the attack in which Billy could create a certificate through a Certificate Authority (CA). This method would be used in conjunction with a Web Proxy Auto-Discovery Protocol (WPAD) exploit to achieve the same goal of unfettered access to all of Peter's unencrypted traffic. This latter attack is rather common as some browsers (and the administrators that configure them) use WPAD in Local Area Network (LAN) settings. To exacerbate the problem, some trusted CA companies had been compromised through social engineering or lax processes in issuing certificates to unauthorized users (such as Billy).
If a MiTM attack cannot launch, Billy has some more complicated attacks he can fall back on which all offer the promise of unencrypted traffic with varying degrees of success and completeness. Browsers use Pseudo-random number generator (PRNG) algorithms to encrypt traffic. If this PRNG is predictable in some way, an attacker could gain access to unencrypted traffic. In a similar vein, attackers can exploit side-channel information – such as a compression side-channel attack. This particular side-channel attack involves sending guesses about the encrypted data to the server and monitoring if the compressed data sent back is smaller – which, if using a common compression algorithm, would indicate that the guess is correct. The attack proceeds by fixing the first (now verified) correct guess and proceeding with the second guess.

#### Security Requirements

To prevent the attacks described in the Misuse Case section, there are several features Peter expects from the Brave Browser. To prevent MiTM attacks, the Brave Browser has features to let him know when he is not using a certificate issued by a trusted CA. The browser can also by default disable the WPAD feature to prevent the MiTM variation involving this protocol. To prevent PRNG attacks, a known secure PRNG algorithm such as ChaCha20 should be used. Lastly, to prevent side-channel attacks, the browser should avoid returning useful timing or size information when compressing data. Furthermore, one site's javascript code should not be able to perform side-channel attacks on another site using privileged side-channel attacks like SPECTRE. SPECTRE relied on the fact that all sites open in a browser (along with their javascript code) run in the same process. The attack leveraged this, along with some hardware design decisions to spy on other sites open in the browser. To mitigate this attack without replacing the hardware, one solution is to use Site Isolation, which runs each site open in the browser in a separate process, preventing an attack like SPECTRE.

#### Diagram

![SSL_Misuse_Cases](https://user-images.githubusercontent.com/31263469/65651646-aa9d3100-dfd4-11e9-82ed-23ff0a1396a9.PNG)

### Password Manager Use Case

#### Use Case

Peter, the privacy-minded user, understands the importance of utilizing strong, complex, and long passwords, but he needs access to several different places and in a quick fashion. Bobby Joe doesn’t want to have to remember several different passwords and doesn’t want to have one password for all sites. He has decided to store all his passwords in the Brave browser built-in password manager. Brave allows the ability to add third-party password managers so Peter could install LastPass to enable more secure password manager. If Peter uses a third-party manager, he must delete/disable Brave’s built-in password manager.

#### Misuse Case

Billy, the hacker, wants to exploit any vulnerabilities that the built-in password manager may have so he can gain access to all Billy’s passwords. Billy can create a fake login form using a third-party JavaScript (cross-site scripting attack) on the most visited website in attempts to steal Peter’s credentials. 

#### Security Requirements
- *still need to finish*

#### Diagram
<img width="916" alt="Screen Shot 2019-09-25 at 7 44 13 PM" src="https://user-images.githubusercontent.com/54923995/65649617-efbd6500-dfcc-11e9-911b-ddad546e6642.png">

### Wallet Use Case

#### Use Case
Peter, the privacy-minded user, needs to use a web browser that allows users to take full control of where advertising revenue is going, while still having their privacy respected. Peter uses the Brave browser to accomplish this, taking full advantage of Brave's reward program that uses Basic Attention Token (BAT). The Brave browser will tally the attention a user would spend on a site they visited and divides up a monthly BAT contribution. Peter can now have full control of who he wishes to contribute to using the BAT's collected or personally funded through the Brave wallet.
 
#### Misuse Case
Billy, the hacker, wants to steal the funds Peter has collected, disrupting the ability for Peter to take full control of his advertisement support. Billy, the hacker, notes that there is a wallet in place, which is where the BAT’s are collected and held for distribution. Billy, wants to hijack this account by setting up a man-in-the-middle attack. Setting up this attack would allow Billy to analyze transactions to alter. Billy also wants to execute malicious code in the Browser to further disrupt Peter’s wallet functionality. 
#### Security Requirements
Due to the exploitations Billy the hacker wants to attempt, Peter, the privacy-minded user expects the Brave browser to keep the integrity the advertisement rewards implementation secure. Brave allows for users like Peter, to earn Basic Attention Tokens (BAT) to collect while surfing the web and store in the Brave wallet. Billy, the hacker is aware of this and will setup a man-in-the-middle attack to analyze transactions made. This would allow Billy to alter transactions. Peter expects the Brave browser to encrypt transactions that are made in case this attack has taken place. Billy. the hacker can also exploit vulnerabilities in the browser by injecting malicious code in order to attempt to steal the further funds in the wallet. Peter expects the Brave browser to have a mechanism of blocking any scripts inserted by the Billy which threatens the availability to use the Brave wallet feature. Lastly, Peter expects the Brave browser to validate the user making transactions, to further prevent Billy from hijacking the account. 
 

#### Diagram 
![Use Case Diagram - Wallet 2 0 (4)](https://user-images.githubusercontent.com/45551925/66014889-2516f680-e496-11e9-8a8a-3bcd52d28cad.png)


### Third-Party Extensions Use Case

#### Use Case 
Peter, the privacy-minded user, wants the ability to customize the Brave browser to their desire. As a result, the Brave browser gives users the option to install third-party extension, which gives the user a customizable experience.   

#### Misuse Case 
Billy, the hacker, wants to disrupt the browser customization, which includes installing malicious extensions without the users knowledge. This entails the creation of a malicious extension, allowing a malicious author to publish and simply wait for a user to download the creation. Billy, the hacker, will conduct this attack by appearing like a legitimate non-threatening author; when in the end, they are truly acting malicious once their extension has been downloaded and installed.   

#### Security Requirements
Peter, the privacy-minded user, expects the Brave browser to have the ability to prevent malicious actors from being able to upload malicious extensions to the platform. Peter expects their to be a process of validating the extensions that are uploaded. Also, Peter expects the Brave browser to block any malicious extensions that installed as another form of protection. The Brave browser would need to review authors who are creating extensions and further mitigate any malicious extensions when installed to prevent Billy the hacker from disrupting the ability to customize the browser to Peter’s choosing.  


#### Diagram
![Use Case Diagram - 3rd party ext 2 0 (1)](https://user-images.githubusercontent.com/45551925/66016149-12eb8700-e49b-11e9-8de5-987a2deb7d5f.png)



## Observation Review of OSS Project Documentation for Security-Related Configuration and Installation Issues

- Assess alignment of security requirements with advertised features of the software. Review OSS project documentation and codebase to support your observations.

By default, first party cookies are not blocked as they are typically needed to log into a given site.  This means that sites like Google can use to track users while on their domain.  
(https://support.brave.com/hc/en-us/articles/360022806212-How-do-I-use-Shields-while-browsing-).  Some users do not like this, but they can use site specific settings or third party extensions to block first party cookies by default.

There are also open issues that seem to indicate that some third party cookies are accepted due to a race condition: 
https://github.com/brave/brave-browser/issues/2223

There are also reports that users have explictily disabled sites like FaceBook from running scripts on the browser, to find out there is a "secret whitelist" enabling FaceBook to run scripts, ignoring the user setting: 
https://community.brave.com/t/how-to-disable-facebook-twitter-secret-whitelist/44961


- Review OSS project documentation for security-related configuration and installation issues. Summarize your observations.

todo: peruse FAQs for any manual setup needed / what defaults are chosen, etc. https://community.brave.com/c/faq

Brave allows users to configure "Shields" that are the differentiators for this browser.  These shields currently control ad blocking, script permissions, connection type (http or https), cookie policies, and tracking protections.
(sources: 
https://support.brave.com/hc/en-us/articles/360022806212-How-do-I-use-Shields-while-browsing-, https://github.com/brave/brave-browser/issues/1288)






- > Link to your team GitHub repository that shows your internal project task assignments and collaborations to finish this task.
