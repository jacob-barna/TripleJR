## CYBR 8420 - Requirements for Software Security Engineering

**Github Repository: https://github.com/jacob-barna/TripleJR**

**Authors:** Jeffrey Smith, Ronald Ramirez, Jacob Barna, Jill Lenz

**Team Name:** TripleJR

## Backstory
short intro/description about Brave and begin to introduce this assignment (see info below Use case 1) .  

Brave is an open source web browser that secures users privacy while still providing a fast browsing experience. The Brave browser blocks all advertisements and tracking mechanisms sites implement to provide a “better” experience to the users using their site. 
* More info should go here 

The stakeholders in our scenarios are primarily users who have privacy in mind. Users using the Brave browser simply want to browse the web without being tracked or have advertisements popup. 
* More info should go here 


### Use Case 1
A markdown report that describes the following:

- Identify five essential data flows (source-transformations-sink) through the software. Develop use-cases diagrams related to these data flows. 
    - Make sure you have a back story in your operational environment. Where is this system being used? What is its criticality? Who are the stakeholders?
    - Ideally, the dataflows need to be spread across different external interactors (humans or systems) of your software. Once different external interactors have been identified, the use cases can focus on the most sensitive features used by the external interactor.

- Derive security requirements for the use-cases using misuse case diagrams. Briefly describe the analysis in each misuse case diagram.
    - The misusers should be contextualized in your environment of operation and relevant to the dataflows identified above. Use names that help the reader understand their motives, resources, attack of choice, and the available access to the system to carry out their attack.
    
### Use Case 2 

### Use Case 3

### Use Case 4 - Wallet Scenerio

#### Use Case
Peter the privacy-minded user, needs to use a web browser that allows for users to take full control of where advertisement revenue is going, while still having their privacy respected. Peter uses the Brave browser to accomplish this, taking full advantage of Brave's reward program that uses Basic Attention Token (BAT). The Brave browser will tally the attention a user would spend on a site they visited and divides up a monthly BAT contribution. Peter can now have full control of who he wishes to contribute to using the BAT's collected or personally funded through the Brave wallet.

#### Misuse Case
Billy the hacker, wants to exploit any vulnerabilities in the browser, specifically targeting the ability for a Peter to take full control of his advertisement support. Billy the hacker, also notes that there is a wallet in place, which is where the BAT’s are collected and held for distribution. 

* more info will go here about preventions and threats that follow 
#### Diagram 
<img width="752" alt="Screen Shot 2019-09-22 at 1 48 01 AM" src="https://user-images.githubusercontent.com/45551925/65383424-17fe4880-dcdb-11e9-9f97-ec09de978798.png">





### Use Case 5


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

## Rubric 

![image](https://user-images.githubusercontent.com/45551925/65192235-ffbcce00-da3b-11e9-83e3-6ff43a87f146.png)
