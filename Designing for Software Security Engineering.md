## CYBR 8420 - Designing for Software Security Engineering  

**Github Repository: https://github.com/jacob-barna/TripleJR**

**Authors:** Jeffrey Smith, Ronald Ramirez, Jacob Barna, Jill Lenz

**Team Name:** TripleJR

Submit a markdown report that includes the following:

* Threat models for critical data-flows through the software. Misuse and assurance cases will provide starting points for examination. Include threat model diagrams. For details see: https://robinagandhi.github.io/swa/slides/lecture-4/design-for-software-se.html#66 (Links to an external site.) 
* Using threat model analysis, review OSS project for design-related issues. Summarize your observations.
* Link to your team GitHub repository that shows your internal project task assignments and collaborations to finish this task. Also, include a summary of your team reflection meeting. What issues occurred? What did you plan to change moving forward?

### Rubric  
![image](https://user-images.githubusercontent.com/45551925/67908013-d6698480-fb47-11e9-821b-0c25ada8041d.png)


### Threat Modeling Data Flow 1: SSL Browsing
* Level 0 DFD  
![SSL_Level_0](https://user-images.githubusercontent.com/31263469/68427554-f7e1f600-016f-11ea-9373-56fccd2d0b4e.png)

* Level 1 DFD  
![SSL_Level_1](https://user-images.githubusercontent.com/31263469/68427555-f9abb980-016f-11ea-9f29-8426b67398f0.png)

* Analysis  
The full report is available here:  
https://github.com/jacob-barna/TripleJR/blob/master/ThreatModels/SSL_Full_Report.htm

### Threat Modeling Data Flow 2: Certificate Revocation List Update
* Level 0 DFD  
![CRL_Update_Level_0](https://user-images.githubusercontent.com/31263469/68427541-f31d4200-016f-11ea-9264-45de4ca55490.png)

* Level 1 DFD  
![CRL_Update_Level_1](https://user-images.githubusercontent.com/31263469/68427550-f6183280-016f-11ea-93ba-3f156a7266d7.png)

* Analysis  
The full report is available here:   
https://github.com/jacob-barna/TripleJR/blob/master/ThreatModels/SSL_Full_Report.htm

### Threat Modeling Data Flow 3: Wallet (Rough Draft)
* Level 0 DFD  
![wallet_level0](https://user-images.githubusercontent.com/45551925/68093384-a75e5600-fe5a-11e9-9e04-a75ed84b7691.png)

* Level 1 DFD  
![wallet_level1](https://user-images.githubusercontent.com/45551925/68093393-bba25300-fe5a-11e9-9dc1-7e26f5962763.png)

* Analysis

### Observation Summary
## Spoofing

In the context of browsing the web using SSL, the Brave browser mitigates the threat of spoofing through the use of secure encryption algorithms.  Brave uses well-known certificate verification routines to trace a certificate to a root Certificate Authority (CA).  If a path to a root CA cannot be verified, the browser warns the user of unsafe communications.  To address unintended information disclosure through spoofing, the browser uses Diffie-Hellman key exchange and secure symmetric algorithms, such as ChaCha20, once a connection is established [1] [2].  This makes decrypting any intercepted traffic improbable.  

There are some recent attacks that leverage the WPAD protocol and could potentially lead to a Man-in-the-middle (MitM) attack.  These should be investigated further.  From searching the Brave repository it does not appear that they override the default setting to enable WPAD on chrome.

In the context of certificate verification, there may be some investigation needed into whether the local certification revocation list can be spoofed.  Initial experiments in this area show that some of the file is in plain text and can be modified (for example, to remove an entry in the revoked CRLs).  It is yet to be proven that such a removal would lead to Brave trusting the certificate.  In addition, even if it were proven that this were the case, the private key of the revoked certificate would need to be in the hands of an attacker, and potentially, the attacker would need to perform a denial of service on the CRL update mechanism on chrome to prevent the CRL list from updating.  

## Tampering

As mentioned in the observations on mitigating spoofing, the Brave browser prefers Elliptic-curve Diffie-Hellman Ephemeral key exchange over other options.  The ephemeral key provides forward secrecy so that if the private key of the communicating party is leaked, the past messages are still secret.  If this cipher suite is implemented correctly, the key exchange is encrypted using the public key of the receiver and can only be decrypted using the private key [3].  During the key exchange, the message containing the public key is signed by the communicating party so the key can be authenticated by the receiver.  If the public key is tampered with, the receiver will know.  After the secret key is exchanged and symmetric encryption has begun, any tampering will result in a garbled message closer to random bits than the original content (avalanche effect).

## Repudiation

Brave does not log unless a switch is used.  This could lead to repudiation, but it may also be desirable to privacy minded users.

## Information Disclosure

Brave browser applies the encyrption schemes described above to prevent information disclosure when crossing trust boundaries.  Any intercepted information is unreadable to an attacker.

## Denial of Service

Denial of service attacks are usually aimed at the network services that the browser uses.  This being said, there are few protections in Brave (and few expected) for these types of attacks.  One exception, in the context of certificate verification (a core duty of the browser), is that the Certificate Revocation List is available locally, so this feature would work (albeit with potentially stale data) even if the updater or CRL repository were unavailable.

## Elevation of Privilege

Brave browser runs by default in a non-privileged mode.  If a user (who is an administrator) opens the chrome process in a higher privilege level, there are serious (recent) vulnerabilities that could allow remote code execution [4].  Most mitigation strategies rely on the user running in least privilege mode and user awareness of the security consequences of clicking untrusted links or visiting untrusted websites as new attacks are constantly found and patched.  Brave browser also mitigates these through a bug bounty program, a security team in place, and constant updates as attacks are found and blocked.  

### Team Reflection Summary
* What went well: 
--Jacob - Extra time for assignment
--Jacob - Lots of research, lots of learning

* What didn't go well: 
--Jacob - problems with Threat modeling tool 2016 deleting data and freezing

* Things we should try: 
-- Jacob - no ideas

## Team GitHub 
[Team Repo](https://github.com/jacob-barna/TripleJR)  
[Team Project Board](https://github.com/jacob-barna/TripleJR/projects/4)  

[1]: https://cs.chromium.org/chromium/src/net/cert/cert_verifier.cc?q=certificate+verifier&sq=package:chromium&dr=CSs
[2]: https://cs.chromium.org/search/?q=chacha&sq=package:chromium&type=cs
[3]: https://www.ei.ruhr-uni-bochum.de/media/nds/veroeffentlichungen/2015/09/14/main-full.pdf
[4]: https://www.cisecurity.org/advisory/multiple-vulnerabilities-in-google-chrome-could-allow-for-arbitrary-code-execution_2019-118/
