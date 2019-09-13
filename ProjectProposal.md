**Cyber8420 Project Proposal**

**Github Repository: https://github.com/jacob-barna/TripleJR**

**Authors:** Jeffrey Smith, Ronald Ramirez, Jacob Barna, Jill Lenz

**Team Name:** TripleJR

* #### An assumed/hypothetical operational environment (e.g., home, office, enterprise, bank, government, etc.) where the users will expect security functionality from the software in its intended use.  
The browser is intended to provide privacy, security, and an alternative approach to monetizing the web. Because of the wide adoption of standard browsers, with "other" browsers sharing just 3.5% of the world-wide market share [1], the current target market appears to be privacy-minded users who use the browser at home, on their mobile devices, or at work if permitted. These users may have philosophical reasons for their aversion to browser tracking. Also, they may wish to keep their activities private from the prying eyes of their government or hacker groups [2].

* #### What are the security needs of users from this software in its intended threat environment ? If there are none or very few, then re-evaluate your selection.  
The security needs for such users start with privacy and security in the core use case of the browser -- browsing the Internet. As mentioned above, some browsers leave user activity unencrypted and vulnerable to snooping. Brave browser must adequately encrypt user data to the browser to prevent such snooping. Brave offers this through the "Private Tabs with Tor" feature. Similarly, users may not want to have a "profile" of their activity built using fingerprinting, described on the Google Chromium Blog as "user-tracking efforts ... employing harder-to-detect methods that subvert cookie control" [3]. Users also expect Brave to protect them from malicious scripts and cross-site scripting attacks, which could lead to security breaches (such as the theft of credentials). Perhaps even more importantly, users expect that any advertiser network built by Brave to be free from malicious software -- which is a promise that networks like DoubleClick have not been able to keep [4].  

Brave also offers several built-in features that users expect to be secure.  One such feature is the Brave password manager.  Users expect the password manager to securely store their credentials so that they may not be recovered except by those authorized.  Another feature is the Brave wallet, which is intended to secure a new Basic Attention Token (BAT) cryptocurrency earned by users or deposited by users for the purpose of contributing to (tipping) content producers.  Brave promises that attack users' wallets cannot come from attacks on their servers, and they note that all transactions must clear their settlement process, which may provide some course of action in the case a keypair is compromised through other means.  If a user decides to contribute cryptocurrency to a content provider, they expect this transaction to be anonymous and recorded correctly (meaning there is no chance that the funds can be misdirected).  To tackle the anonymity challenge, Brave uses the Anonize2 protocol [5].  To ensure that transactions are recorded properly, Brave uses the Ethereum platform, a cryptocurrency built on the assumption (as with all decentralized cryptocurrency) that no one will ever control 51% of the networks hash rate.  This assumption may not be so safe as the recent activity has caused at least one cryptocurrency exchange to pause Ethereum transactions for fear of such an attack [6].  Besides attacks on the currency itself, users and exchanges have also suffered billions of dollars of losses in wallets [7].  Brave must provide a secure wallet to ensure that such theft does not originate from their software.

One last concern not explicitly discussed by Brave deal with the privileges that are granted to Brave.  Brave promises to keep your data secure and anonymous in several areas: when gathering advertising data, when sending tips to content providers, and when syncing bookmarks and settings.  How can one assure themselves that a Brave insider will not use their position to merge malicious code and steal data or cryptocurrency?  Brave points out that they produce open-source software which can be audited by anyone to answer these concerns [8].  Is that enough? We have seen many examples of people using such an attack vector to spread malware [9].  In a similar vein, there has been some chatter about the trust that must be placed in Brave.  For example, to some users, Brave acts as a "mafia" by controlling access to your cryptocurrency [10] for 90 days if they suspect fraud or malicious activity.  There has also been a concern that Brave has "whitelisted" ad trackers for companies like Facebook [11], which may or may not allow Facebook to track user data. 

* #### Develop a list of security features in the software. Again, if there are none or very few, then re-evaluate your choice.
As discussed above, the Brave browser project focuses primarily on privacy and security. The following are are security features that browser contains [12].

* Ad Blocking [13]
* Fingerprinting Prevention
* Cookie Control
* HTTPS Upgrading
* Block Scripts [14]
* Per-Site & Global Sheild Settings/Defaults
* Clear Browser Data
* Password Manager
* Form Autofill
* Control Content Access To Fullscreen Presentation
* Control Site Access To Autoplay Media
* Send "Do Not Track" With Browsing Requests
* Hardware Security Key Support (YubiKey) [15]

In addition to the features above, Brave does not access data that is user identifiable and all ad campaign data collected is anonymized for the purpose of reporting and accounting. The browser does track user activities inside the application, however the code contains this information on the client device and does not allow server access to this data [16]. This feature of having a private system in which the browser preserves privacy is what Brave has named Privacy-Preserving Product Analytics (P3A) [17].

* #### Motivation for selecting this project.   
As information technology students, we have seen many digital advancements in technology. We are living in an era where our online data is being sold to companies to promote products and target specific content to us, the users. Security and privacy are characteristics we value highly, and hope companies hold their promises when saying they do so as well. However, trusting companies becomes more difficult for us to do. Previous outbreaks which include tech conglomerates such as Facebook were fined $5 billion for violating consumers’ privacy rights [18]. Finding solutions to keep our privacy and security as we utilize technology and different online outlets is something we strive to do.  

A solution that users could look into happens to be an open-source web browser application called Brave. The Brave browser allows users to enjoy private, secure, and fast browsing. Our group is determined to conduct an analysis of this application throughout the semester and determine whether the Brave application holds up to their security features they present. We also feel that other users who value privacy and security can relate to this project, which is why we have assumed an environment that targets users who would be using a desktop or mobile device in a home setting or even work if permitted. As we move along throughout the semester, we hope that we are able to successfully assess this open-source application and even provide contributions to the Brave community. 

* #### Open source project description (What is it?, Contributors, Activity, Use, Popularity, Languages used, platform, documentation sources, etc.)   

As we briefly described, the Brave application is an open-source web browser application that integrates privacy, security, and fast browsing. This application is written in 96% JavaScript but includes other languages like python as well. The project is relatively popular in the world of web browsers. It has over 3,800 stars, 350 forks, with thousands of issues waiting to be closed. 

![Screen Shot 2019-09-10 at 8 45 01 PM](https://user-images.githubusercontent.com/45551925/64661891-1647a180-d40c-11e9-8586-6819ef990b05.png)

The Brave application also provides a variety of instruction sets depending on what operating system the user is wishing to install the application. The application is available on all platforms, covering desktop users such as macOS, Windows, Linux, as well as mobile users on iOS and Android. The GitHub repository for the Brave application also includes helpful templates for users who wish to contribute, by adding templates for how to open an issue and creating a pull request. Lastly, from our brief interaction with this open-source web browser, we noticed that they also have a community page for users who would like to get more involved with Brave. Here, users can ask for assistance and even discuss features that should be implemented into the application.

* #### Discuss License, procedures for making contributions, and contributor agreements. 
The Mozilla Foundation is currently the license steward for The Brave project and holds all rights in regards to modifying or publishing new versions of the license. All licenses under this steward must be adhered to and can only be modified by another entity other than the steward when the software is developed that is not governed under the current Brave license. Contributions are permitted and each contributor is granted a worldwide, royalty-free, non-exclusive license. Contributors are permitted to use, modify, and distribute the source code with the exceptiong that all source code used must comply with the license agreement and users must be made aware of the location of the original Brave license. In the event a contributor distributes an executable form of the software, then the source code and original license must be made available to users. Failing to comply with the terms set forth in the license will result in contributors having their rights terminated with the possibility of reinstatement once back in compliance [19].

Contributions to the Brave project are active and supported by the community. All levels of contributor experience regarding the open-source software contribution are welcomed with several categories available depending on interests. Basic contributions can be made by supporting others or attempting to replicate reported issues. Other contribution categories include quality assurance, development, and design. By assisting in these categories, contributors can assist with automation features, compatibility checks and testing, resource developments, and usability testing or research. To further assist potential contributors, the Brave community provides contact names for each aspect of contributions that can be contacted to provide guidance and assistance with contributions that are of interest. This can be completed by creating an account on their support community website or through contributions on their GitHub repository [20].

* #### Summary of security-related history for the software (E.g., known vulnerabilities, security-related engineering decisions, security feature additions/removal, etc. ). 

Since the launch of Brave Software back in January of 2016, Brave has had many notable additions to their software.  In June 2018, Brave released a pay-to-surf test version of the browser [wiki?]. The Brave browser blocks tracking scripts and many web ads.  However, Brave gives the users the option to see ads but as desktop notifications rather than directly on the website the user is visiting. In return for turning this option on, the user gets 70% of the revenue they generate. (https://www.wired.com/story/brave-browser-will-pay-surf-web/)

Later in June of 2018, Brave added support for Tor in its desktop browser’s private browsing mode [cite].  Brave called this technology onion routing, and it gives the ability for the user to stay anonymous by shuttling the internet communications by obscuring the true address of the Internet [cite].(https://www.cnet.com/news/brave-advances-browser-privacy-with-tor-powered-tabs/)

Until December 2018, Brave replaced Muon interface and moved to Chromium codebase that does support Chrome extensions. (https://www.zdnet.com/article/brave-browser-moves-to-chromium-codebase-now-supports-chrome-extensions/)

In June 2019 Brave started testing new ad-blocking rule matching algorithm implemented in Rust that Brave claims are on average 69 times faster than the previous implementation in C++ [wiki?]

Other milestones for the Brave browser can be found here: (https://github.com/brave/brave-browser/wiki/Roadmap-Archive)

Brave browser has had two known vulnerabilities back in 2017 and 2018.  In 2017, browser version 0.19.73, and earlier, was vulnerable to an incorrect access control issue in the “JS fingerprinting blocking” component, resulting in a malicious website being able to access the fingerprinting-associated browser functionality [cite].  In 2018, the browser in iOS before 1.2.18 and Brave Browser Android 1.9.56 and earlier suffered from Full Address Bar Spoofing, allowing attackers to trick a victim by displaying a malicious page for legitimate domain names [cite]. Both vulnerabilities were resolved within 30 days or less. (https://www.cvedetails.com/vulnerability-list/vendor_id-16266/product_id-36540/Brave-Browser.html)

* ####[Link to your team GitHub repository that shows your internal project task assignments and collaborations to finish this task.](https://github.com/jacob-barna/TripleJR)
* #### Github Project Boards . 
* #### Kanban boards . 

[1]: https://gs.statcounter.com/browser-market-share#monthly-200901-201905
[2]: https://www.fastcompany.com/3058432/the-top-3-web-browsers-in-china-leave-users-vulnerable-report-says
[3]: https://blog.chromium.org/2019/05/improving-privacy-and-security-on-web.html
[4]: https://www.forbes.com/sites/leemathews/2018/01/26/hackers-abuse-google-ad-network-to-spread-malware-that-mines-cryptocurrency/
[5]: https://anonize.org/
[6]: https://cointelegraph.com/news/ethereum-classic-51-attack-the-reality-of-proof-of-work
[7]: https://www.computerworld.com/article/3389678/whats-a-crypto-wallet-and-does-it-manage-digital-currency.html
[8]: https://brave.com/faq/#concerns
[9]: https://hackaday.com/2018/10/31/when-good-software-goes-bad-malware-in-open-source/
[10]: https://thenextweb.com/hardfork/2018/11/23/brave-blockchain-cryptocurrency-browser/
[11]: https://nakedsecurity.sophos.com/2019/02/12/privacy-browser-braves-user-concern-over-facebook-whitelist/
[12]: https://brave.com/features/
[13]: https://brave.com/improved-ad-blocker-performance/
[14]: https://brave.com/script-blocking-exceptions-update/
[15]: https://brave.com/partnership-with-yubico/
[16]: https://brave.com/faq/
[17]: https://brave.com/privacy-preserving-product-analytics-p3a/
[18]: https://www.usatoday.com/story/tech/news/2019/07/24/facebook-pay-record-5-billion-fine-u-s-privacy-violations/1812499001/
[19]: https://raw.githubusercontent.com/cyb3rc0wb0y/brave-browser/master/LICENSE
[20]: https://community.brave.com/t/about-the-contributing-category/1891
