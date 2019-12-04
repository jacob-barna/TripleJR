## CYBR 8420 - Code analysis for Software Security Engineering    

**Github Repository: https://github.com/jacob-barna/TripleJR**

**Authors:** Jeffrey Smith, Ronald Ramirez, Jacob Barna, Jill Lenz

**Team Name:** TripleJR

Code analysis for Software Security Engineering: A markdown report that describes the following:

- A short summary of your code review strategy.
-- What challenges did you anticipate and how did your code review strategy attempt to address those challenges?
- Findings from manual code review of critical security functions identified in misuse cases, assurance cases and threat models.
- Findings from automated code scanning (if available). Include links to full reports.
- Summary of key findings from manual and/or automated scanning. This summary may include categorization, mappings to CWEs, CAPECs, Risk Levels, etc.
- Links to any pull requests, issues, discussion, etc. from the team to the original project and any follow-up interactions.
- Link to your team GitHub repository that shows your internal project task assignments and collaborations to finish this task. Also, include a summary of your team reflection meeting. What issues occurred? What did you plan to change moving forward?  

Can be deleted before submission/from textbook and things to consider: A code security review helps you find possible security flaws, share knowledge of how to design secure code, and improve the overall design.  the overall design of the code, while paying extra attention to things like the implementation or absence of secure code constructs. Another aspect to think about is which people should take part in the code security review. Should you only involve people within the team, or should you also include people from outside the team?

## Rubric 
![image](https://user-images.githubusercontent.com/45551925/69557223-d8b6d700-0f6b-11ea-997b-96c15819f889.png)

## Code Review Strategy 

### Security features that should be involved in the code review:
* CNAME verification 
* Use of first party cookies and blocking of third-party cookies 
* Block scripts 
* Use SSL
* Use strong default settings
* Authorization methods
* Use encryption
* Require strong passwords

### Below is an overview of our strategy:
* Identify source code security problems with automated analysis
* Analyze the findings from automated analysis
  * Map findings to any patterns from the analysis. 
* Run static analysis tools against the codebase
* Analyze the findings from static analysis 
  * Identify any patterns from the analysis. Identify repeated CWEs. 
* Perform manual code review of notable security features from our assurance cases, use and misuse cases
* Map findings to threats related to CWEs identified in automated and static analysis.


## Code Review Results

### Manual Code Review   
#### SSL use/misuse cases
  
### Automated Code Scanning  
The first tool we used to analyze the Brave tool was [Codacy](https://www.codacy.com/). The tool was able to find 1086 total issues. The brakedown of these issues includes the following:

- Security = 27
- Error Prone = 16
- Code Style = 1043

Our team first began to look more into the large number we received back for the Code Style. When seeing this, our initial thoughts were that the “issues” flagged for this section would probably include a lot of “code grammer.” And after reviewing, it was in fact the case. For example, in the following path: “scripts/lint.py” the code picked up a few silly “issues.” 

<img width="668" alt="codacy-1" src="https://user-images.githubusercontent.com/45551925/69897430-9f86ba00-1311-11ea-89f5-f9661265a600.png">

Another “issue” we noticed during our automated testing was that during the following path: “lib/build.js” the code picked up an error for not using a semicolon. 

![issue2-SA](https://user-images.githubusercontent.com/45551925/70160691-861e9e80-1680-11ea-8c38-4e51d2f77b3b.png)

However, with JS it is best practice to use depends on the statement written since it doesn’t always need a semicolon to run, but it is best practice.  [Link to JS semicolon article](https://dev.to/adriennemiller/semicolons-in-javascript-to-use-or-not-to-use-2nli) 

Next, we began looking at our results at the issues noted for “Error Prone.” From our results we noticed that most of the issues for this contained information about the functions complexity. As this issues states, these issues are noted to emphasis on conducting a simplification on the line of code. For more information on how a user limiting complexity, see the [article here.](https://eslint.org/docs/rules/complexity) 

![issue3-SA](https://user-images.githubusercontent.com/45551925/70160782-aa7a7b00-1680-11ea-88c7-41e52e1df5cf.png)


### Summary of Key Findings from Manual/Automated (Mappings to CWEs, CAPECs, Risk Levels, etc.) 
- Jill: Not a whole lot of time to discuss in class together but we are able to communicate everything we need through discord and github.  We have separated tasks to give indivdually. 


## Team GitHub 
[Team Repo](https://github.com/jacob-barna/TripleJR)  
[Team Project Board](https://github.com/jacob-barna/TripleJR/projects/5)  
