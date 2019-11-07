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

In the context of browsing the web using SSL, the Brave browser mitigates the threat of information disclosure through the use of secure encryption algorithms.  Brave uses well-known certificate verification routines to trace a certificate to a root Certificate Authority (CA).  If a path to a root CA cannot be verified, the browser warns the user of unsafe communications.  In the context of information disclosure, the browser has a secure encryption scheme using Diffie-Hellman routines [1] for key exchange and secure symmetric algorithms, such as ChaCha20 once a connection is established [2].  This makes decrypting any intercepted traffic improbable.  

There are some recent attacks that leverage the WPAD protocol and could potentially lead to a Man-in-the-middle (MitM) attack.  These should be investigated further.  From searching the Brave repository it does not appear that they override the default setting to enable WPAD on chrome.


## Tampering

## Repudiation

## Information Disclosure

## Denial of Service

## Elevation of Privilege

### Team Reflection Summary
* ...

## Team GitHub 
[Team Repo](https://github.com/jacob-barna/TripleJR)  
[Team Project Board](https://github.com/jacob-barna/TripleJR/projects/4)  

[1]: https://cs.chromium.org/chromium/src/net/cert/cert_verifier.cc?q=certificate+verifier&sq=package:chromium&dr=CSs
[2]: https://cs.chromium.org/search/?q=chacha&sq=package:chromium&type=cs
