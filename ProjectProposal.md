### Project Proposal: 2-3 page markdown document that describes the following:  

* #### An open-source software project your team has chosen. From here on, it will be referred to as “software”. 
Our idea that we will be going with if everyone is okay with this.
https://github.com/brave/brave-browser

* #### An assumed/hypothetical operational environment (e.g., home, office, enterprise, bank, government, etc.) where the users will expect security functionality from the software in its intended use.  

This browser is intended to provide privacy, security, and an alternative approach to monetizing the web.  Because of the wide adoption of standard browsers, with "other" browsers sharing just 3.5% of the world-wide marketshare [1], the current target market appears to be privacy-minded users who will use the browser at home, on their mobile devices, or at work if permitted.  These users may have philosophical reasons for their aversion to browser tracking, or, they may wish to keep their activities private from the prying eyes of their government or hacker groups [2].

* #### What are the security needs of users from this software in its intended threat environment ? If there are none or very few, then re-evaluate your selection.  
The security needs for such users starts with privacy and security in the core use case of the browser -- browsing the internet.  As mentioned above, some browsers leave user activity unencrypted and vulnerable to snooping.  Brave browser must properly encrypt user data all the way to the browser to prevent such snooping.  Brave offers this through the "Private Tabs with Tor" feature.  Similarly, users may not want to have a "profile" of their activity built using fingerprinting, described on the Google Chromium Blog as "user-tracking efforts ... employing harder-to-detect methods that subvert cookie control" [3].  Users also expect Brave to protect them from malicious scripts and cross-site scripting attacks which could lead to security breaches (such as the theft of credentials).  Perhaps even more importantly, users expect that any advertiser network built by Brave to be free from malicious software -- which is a promise that networks like DoubleClick have not been able to keep [4].  

Brave also offers several built-in features that users expect to be secure.  One such feature is the Brave password manager.  Users expect the password manager to securely store their credentials so that they may not be recovered except by those authorized.  Another feature is the Brave wallet, which is intended to secure a new Basic Attention Token (BAT) cryptocurrency earned by users or deposited by users for the purpose of contributing to (tipping) content producers.  Brave promises that attacks on users' wallets cannot come from attacks on their servers, and they note that all transactions must clear their settlement process, which may provide some course of action in the case a keypair is compromised through other means.  If a user decides to contribute cryptocurrency to a content provider, they expect this transaction to be anyonymous and recorded correctly (meaning there is no chance that the funds can be misdirected).  To tackle the anonymity challenge, Brave uses the Anonize2 protocol [5].  To ensure that transactions are recorded properly, Brave uses the Ethereum platform, a crypto currency built on the assumption (as with all decentralized crytpocurrency) that no one will ever control 51% of the networks hash rate.  This assumption may not be so safe as recent activity has caused at least one cryptocurrency exchange to pause Ethereum transactions for fear of such an attack [6].  Besides attacks on the currency itself, users and exchanges have also suffered billions of dollars of losses in wallets [7].  Brave must provide a secure wallet to ensure that such theft does not originate from their software.

One last concern not explicitly discussed by Brave deal with the privileges that are granted to Brave.  Brave promises to keep your data secure and anonymous in several areas: when gathering advertising data, when sending tips to content providers, and when syncing bookmarks and settings.  How can one assure themselves that a Brave insider will not use their position to merge malicious code and steal data or cryptocurrency?  Brave points out that they produce open-source software which can be audited by anyone to answer these concerns [8].  Is this enough? We have seen many examples of people using such an attack vector to spread malware [9].  In a similar vein, there has been some chatter about the trust that must be placed in Brave.  For example, to some users, Brave acts as a "mafia" by controlling access to your cryptocurrency [10] for 90 days if they suspect fraud or malicious activity.  There has also been concern that Brave has "whitelisted" ad trackers for companies like Facebook [11], which may or may not allow Facebook to track user data.  

* #### Develop a list of security features in the software. Again, if there are none or very few, then re-evaluate your choice.



* #### Motivation for selecting this project .   
As information technology students, we have seen many digital advancements in technology. We are living in an era where our online data is being sold to companies to promote products and target specific content to us, the users. Security and privacy are characteristics we value highly, and hope companies hold their promises when saying they do so as well. However, trusting companies becomes more difficult for us to do. Previous outbreaks which include tech conglomerates such as Facebook, were fined $5 billion for violating consumers’ privacy rights. [source here] Finding solutions to keep our privacy and security as we utilize technology and different online outlets is something we strive to do.  

A solution that users could look into, happens to be an open source web called Brave. The Brave browser allows users to enjoy private, secure and fast browsing. Our group is determined to conduct an analysis on this application throughout the semester and determine whether the Brave application holds up to their security features they present. From the knowledge that we will obtain throughout the semester, we hope that we are able to provide contributions to this open source application. 

[source here]  Facebook privacy https://www.usatoday.com/story/tech/news/2019/07/24/facebook-pay-record-5-billion-fine-u-s-privacy-violations/1812499001/


* #### Open source project description (What is it?, Contributors, Activity, Use, Popularity, Languages used, platform, documentation sources, etc.)   
 
-should we include images ?   
-references ?   

As we briefly described, the Brave application is an open source web browser application that integrates privacy, security and fast browsing. This application is written in 96% JavaScript but includes other languages like python as well. The project is fairly popular in the world of web browsers. It has over 3,800 stars, 350 forks, with thousands of issues waiting to be closed. (not sure if we should include an image?). The Brave application also provides a variety of instruction sets depending on what operating system the user is wishing to install the application. The GitHub repository for the Brave application also includes helpful templates for users who wish to contribute, by adding templates for how to open an issue and creating a pull request.   


* #### Discuss License, procedures for making contributions, and contributor agreements . 
* #### Summary of security-related history for the software (E.g., known vulnerabilities, security-related engineering decisions, security feature additions/removal, etc. ) . 
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
