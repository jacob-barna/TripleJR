## CYBR 8420 - Requirements for Software Security Engineering

**Github Repository: https://github.com/jacob-barna/TripleJR**

**Authors:** Jeffrey Smith, Ronald Ramirez, Jacob Barna, Jill Lenz

**Team Name:** TripleJR
 
 ----------------------
 - need to clean this up
- [Observation Review of OSS Project Documentation for Security-Related Configuration and Installation Issues](#observation-review-of-oss-project-documentation-for-security-related-configuration-and-installation-issues)
 ----------------------


## Backstory

Brave is an open-source web browser that secures users' privacy while still providing a fast browsing experience. The Brave browser blocks all advertisements and tracking mechanisms sites implement to provide a "better" experience to the users using their site. In our hypothetical environment, our targeted users continue to be privacy-minded people who will use the browser in a home or work environment if permitted on desktop and mobile devices.  

These users are also considered our stakeholders. Users using the Brave browser want to browse the web without being tracked or have advertisements popup, all while having privacy in mind. The Brave browser also provides a built-in password manager and autofill capabilities to allow our stakeholders to manage their passwords for their desired applications securely. Stakeholders are also looking for automatic upgrades to HTTPS, whenever possible to encrypt the communication. The Brave browser will do its best to upgrade standard unencrypted HTTP communication line, to a secure HTTPS medium. These are all features that our privacy-minded stakeholders' value deeply and are looking for in a web browser in the digital age today. 

With that being said, the five essential data flows that we have analyzed for the Brave browser is the following:
- [Brave Browser Search Use Case](#brave-browser-search-use-case)
- [SSL Use Case](#ssl-use-case)
- [Password Manager Use Case](#password-manager-use-case)
- [Wallet Use Case](#wallet-use-case)
- [Third-Party Extensions Use Case](#third-party-extensions-use-case)

### Brave Browser Search Use Case

#### Use Case

Peter, the privacy-minded user, expects that when utilizing the default search engine defined inside the Brave browser that his privacy is respected. Peter expects the Brave browser’s search engine to not include results that are tracked by third-parties when searched or visited. The Brave browser does not block first-party cookies by default to allow for better user experience while navigating through individual sites to maintain persistence of user activities such as logins and shopping carts. Peter understands that disabling all cookies could result in the loss of these user experiences but the enabling of cookies could led to the possibility of being tracked by third-party cookies or servers.

#### Misuse Case

Billy, the hacker wants to exploit the privacy of the user, Peter, while browsing search engines and websites by tracking the sites and items searched and visited inside the Brave browser. Billy wants to be able to monetize off of Peter's browsing activities by selling it to venders. He also hopes that the data can be used to determine what Peter is interested in to utilize targeted items to lure Peter to malicious sites or downloads. To accomplish this, Billy has determined that he can carry his malicious plan out that includes three different misuse cases. The first misuse case included in exploiting the privacy is through the means of setting Billy’s third-party tracking cookie as a first-party cookie to prevent being blocked on the search engine and browser sites. This will bypass and threaten the default or user settings that attempt to block third-party cookies by being set on Peter's device as a first-party cookie. The second included misuse case action is Billy initializing the third-party tracking cookies inside JavaScript to render and appear as first-party cookies on the search engine and browser. Since the JavaScript is being rendered and executed on the current domain being displayed, Billy can have his third-party cookie used inside the code and appear as a first-party cookie which also threatens the blocking of third-party cookies. The last and final included action Billy can take is by using DNS aliasing to mask his third-party tracking servers as a first-party server. By doing this it threatens the use of first-party cookies and when the third-party server is contacted the DNS aliasing can spoof a first-party server resulting in Peter's device to think that it is a first-party server.

#### Security Requirements

In order to prevent the attacks listed above in the misuse cases, there are features and settings that Peter expects to see included in the Brave browser. To prevent the misuse case of setting third-party cookies as first-party cookies, Brave by default blocks all third-party cookies of domains that are being viewed in the browser. The Brave browser also has custom settings to block all cookies globally or site-to-site which will result in the prevention of this misuse case. Additionally, the misuse case of Billy initializing third-party cookies as JavaScript, that threatens the blocking of third-party cookies, Peter can utilize the settings inside Brave to block the execution of JavaScript’s and therefore preventing the misuse case. This will prevent JavaScript execution, causing third-party cookies to appear as if it is a first-party cookie since the code is being executed on the current domain. Lastly, the misuse case of the third-party cookie server using DNS aliasing, which threatens the use of first-party cookies, Peter can implement CNAME verification to prevent this threat. In doing so, the CNAME records will be verified and the cross-domain tracking of Peter’s activities will be stopped. Implementing these requirements will ensure Peter is getting the privacy he expects from the browser.

#### Diagram

![broswer_use_case](https://user-images.githubusercontent.com/25576618/66060330-1581c700-e503-11e9-9dc1-eaab11b6b30a.png)

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

Peter, the privacy-minded user, understands the importance of utilizing strong, complex, and long passwords, but he needs access to several different places and in a quick fashion. Peter doesn’t want to have to remember several different complex passwords for all the sites he accesses with username and password required. He has decided to store all his passwords in the Brave browser built-in password manager. With the built-in browser in place, Peter can have auto-filled enabled so that when he visits a site, his username and password will automatically appear in the appropriate login fields. He has created different passwords for most of the sites, and those passwords are strong, long, and complex. 

#### Misuse Case

Billy, the hacker, wants to exploit any vulnerabilities that the built-in password manager may have so he can gain access to all Billy’s passwords. One misuse case could arise when Billy creates a fake login form using a third-party JavaScript (cross-site scripting attack) on the most visited website in attempts to steal Peter’s credentials. Another misuse cases that could arise is Billy, the hacker, running a brute force or dictionary attack. The brute force attack would be used to decode the encrypted data of the passwords. The dictionary attack would use a dictionary headword list to generate possible passwords. Another misuse case could be if Billy uses a rainbow table attack in attempts to discover a password from the hash. 

#### Security Requirements

Peter, the privacy-minded user, expects the built-in password manager within the Brave browser to provide him with an easy and secure way to access all his passwords in one place. After all, Brave browser claims to be secure in all their features. To prevent a third-party script attack, Brave browser does block scripts, but Peter would need to make sure that the feature is at the default and not adjusted to allow scripts manually. To prevent brute force, dictionary or rainbow attacks, Peter would still have to make sure he is utilizing different, strong, complex, and long passwords for each site he saves his credentials at. 

#### Diagram

![Use Case Diagram - Password Manager (1)](https://user-images.githubusercontent.com/54923995/66077923-a1591a80-e526-11e9-80a6-784d1068e99f.png)

### Wallet Use Case

#### Use Case
Peter, the privacy-minded user, needs to use a web browser that allows users to take full control of where advertising revenue is going, while still having their privacy respected. Peter uses the Brave browser to accomplish this, taking full advantage of Brave's reward program that uses Basic Attention Token (BAT). The Brave browser will tally the attention a user would spend on a site they visited and divides up a monthly BAT contribution. Peter can now have full control of who he wishes to contribute to using the BAT's collected or personally funded through the Brave wallet.
 
#### Misuse Case
Billy, the hacker, wants to steal the funds Peter has collected, disrupting the ability for Peter to take full control of his advertisement support. Billy, the hacker, notes that there is a wallet in place, which is where the BAT’s are collected and held for distribution. Billy wants to hijack this account by setting up a man-in-the-middle attack. Setting up this attack would allow Billy to analyze transactions to alter. Billy also intends to execute malicious code in the Browser to further disrupt Peter’s wallet functionality. 

#### Security Requirements
Due to the exploitations Billy the hacker wants to attempt, Peter, the privacy-minded user expects the Brave browser to keep the integrity the advertisement rewards implementation secure. Brave allows for users like Peter, to earn Basic Attention Tokens (BAT) to collect while surfing the web and store in the Brave wallet. Billy, the hacker is aware of this and will set up a man-in-the-middle attack to analyze transactions made. This would allow Billy to alter transactions. Peter expects the Brave browser to encrypt transactions that are made in case this attack has taken place. Billy, the hacker, can also exploit vulnerabilities in the browser by injecting malicious code to attempt to steal further funds in the wallet. Peter expects the Brave browser to have a mechanism of blocking any scripts inserted by Billy, which threatens the availability to use the Brave wallet feature. Lastly, Peter expects the Brave browser to validate the user making transactions, to further prevent Billy from hijacking the account. 
 

#### Diagram 
![Use Case Diagram - Wallet 2 0 (4)](https://user-images.githubusercontent.com/45551925/66014889-2516f680-e496-11e9-8a8a-3bcd52d28cad.png)


### Third-Party Extensions Use Case

#### Use Case 
Peter, the privacy-minded user, wants the ability to customize the Brave browser to their desire. As a result, the Brave browser gives users the option to install third-party extensions, which provides the user with a customizable experience.   

#### Misuse Case 
Billy, the hacker, wants to disrupt the browser customization, which includes installing malicious extensions without the users' knowledge. This entails the creation of a malicious extension, allowing a malicious author to publish and wait for a user to download the creation. Billy, the hacker, will conduct this attack by appearing like a legitimate non-threatening author; when in the end, they are truly acting maliciously once their extension has been downloaded and installed.   

#### Security Requirements
Peter, the privacy-minded user, expects the Brave browser to have the ability to prevent malicious actors from being able to upload malicious extensions to the platform. Peter expects there to be a process of validating the extensions that are uploaded. Also, Peter expects the Brave browser to block any malicious extensions that install as another form of protection. The Brave browser would need to review authors who are creating extensions and further mitigate any malicious extensions when installed to prevent Billy, the hacker from disrupting the ability to customize the browser to Peter’s choosing.  

#### Diagram
![Use Case Diagram - 3rd party ext 2 0 (1)](https://user-images.githubusercontent.com/45551925/66016149-12eb8700-e49b-11e9-8de5-987a2deb7d5f.png)



## Observation Review of OSS Project Documentation for Security-Related Configuration and Installation Issues

*Assess alignment of security requirements with advertised features of the software. Review OSS project documentation and codebase to support your observations*

One of the advertised security features listed on the Brave Browser Feature List is the implementation of Shields [1]. This feature includes items such as cookie control, ad blocking, and script blocking. By default, first-party cookies are not blocked as they are typically needed to provide a better user experience and assist with different site functions and activities. This means that sites like Google can use to track users while on their domain [2]. Some users do not like this, but they can use site specific settings or third party extensions to block first-party cookies by default. Brave documentation explains this further and identifies the individual controls and settings to custom tailor the security per-site [3]. This aligns with the security requirement that user’s privacy is a priority and can be explicitly configured for each site that the user visits. Searching the Brave community, it can be seen that the Shield feature has contributions from multiple users along with feature requests to work into future builds [4].

*Review OSS project documentation for security-related configuration and installation issues. Summarize your observations.*

Brave allows users to configure "Shields" that are the differentiators for this browser.  These shields currently control ad blocking, script permissions, connection type (http or https), cookie policies, and tracking protections [3][5].The following code snippet is referenced from the Brave ad-block repository, demonstrating how they block advertisement URL’s [6]. 
```c++
  // Do the checks
  std::for_each(urlsToCheck, urlsToCheck + sizeof(urlsToCheck) / sizeof(urlsToCheck[0]), [&client, currentPageDomain](std::string const &urlToCheck) {
    if (client.matches(urlToCheck.c_str(), FONoFilterOption, currentPageDomain)) {
      cout << urlToCheck << ": You should block this URL!" << endl;
    } else {
      cout << urlToCheck << ": You should NOT block this URL!" << endl;
    }
  });
}
```
Looking through issues, a couple were identified with the Shield which indicate that some third party cookies are accepted due to a race condition [7] and another indicates that there are also reports that users have explicitly disabled sites like FaceBook from running scripts on the browser, to find out there is a "secret whitelist" enabling Facebook to run scripts, ignoring the user setting [8]. 

## Team GitHub 
[Team Repo](https://github.com/jacob-barna/TripleJR)  
[Team Project Board](https://github.com/jacob-barna/TripleJR/projects/2)  

## Brave Resources
[Brave Browser Repo](https://github.com/brave/brave-browser)  
[Brave Website](https://brave.com/)  
[Brave Community Page](https://community.brave.com/)

[1]: https://brave.com/features/
[2]: https://brave.com/faq/#search-engines
[3]: https://support.brave.com/hc/en-us/articles/360022806212-How-do-I-use-Shields-while-browsing-
[4]: https://community.brave.com/search?q=shield
[5]: https://github.com/brave/brave-browser/issues/1288
[6]: https://github.com/brave/ad-block/blob/master/README.md
[7]: https://github.com/brave/brave-browser/issues/2223
[8]: https://community.brave.com/t/how-to-disable-facebook-twitter-secret-whitelist/44961

