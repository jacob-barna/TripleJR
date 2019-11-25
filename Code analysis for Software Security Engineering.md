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

Security features that should be involved in the code review: 
•	CNAME verification
•	Use of first party cookies and blocking of third-party cookies
•	Block scripts
•	Use SSL
•	Use strong default settings
•	Authorization methods
•	Use encryption
•	Require strong passwords
Below is an overview of our strategy:
•	Identify source code security problems with automated analysis
•	Analyze the findings from automated analysis
o	Map findings to any patterns from the analysis. 
•	Run static analysis tools against the codebase
•	Analyze the findings from static analysis 
o	Identify any patterns from the analysis. Identify repeated CWEs. 
•	Perform manual code review of notable security features from our assurance cases, use and misuse cases
o	Map findings to threats related to CWEs identified in automated and static analysis.


## Code Review Results

### Manual Code Review   
- stuff will go here  
  
### Automated Code Scanning  
- stuff will go here  

### Summary of Key Findings from Manual/Automated (Mappings to CWEs, CAPECs, Risk Levels, etc.) 
- Jill: Not a whole lot of time to discuss in class together but we are able to communicate everything we need through discord and github.  We have separated tasks to give indivdually. 


## Team GitHub 
[Team Repo](https://github.com/jacob-barna/TripleJR)  
[Team Project Board](https://github.com/jacob-barna/TripleJR/projects/5)  
