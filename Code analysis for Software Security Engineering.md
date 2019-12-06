## CYBR 8420 - Code analysis for Software Security Engineering    

**Github Repository: https://github.com/jacob-barna/TripleJR**

**Authors:** Jeffrey Smith, Ronald Ramirez, Jacob Barna, Jill Lenz

**Team Name:** TripleJR

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

#### Challenges: 
1 - No one on the team is an expert in C++ development.  
This challenge is overcome by relying heavily on automated scanning.  The team also relied heavily on online sources to learn about the security rules flagged by the analysis tools.  

2 - The codebase is gigantic.  
For manual review, code search was heavily used to target the code to review manually.  This at least narrowed down the code to review manually and allowed for quick navigation between related files.  This is also mitigated by the heavy reliance on automated tools.


## Code Review Results

### Manual Code Review   
#### SSL use/misuse cases

##### Code Review related to Claim C4: the browser uses an encryption scheme suitably resistant to cryptographic attacks

##### Misuse Case: Side channel attack 

There is an official project page describing the mitigations against known side channel attacks:
https://www.chromium.org/Home/chromium-security/ssca

##### Misuse Case: PRNG attack 

There is an official security policy, and in this linked document, the subject of FIPS certification and PRNGS is explained in detail:
https://cs.chromium.org/chromium/src/third_party/boringssl/src/crypto/fipsmodule/FIPS.md?type=cs&q=PRNG+boring&sq=package:chromium&g=0&l=43

The code for the PRNG is found here: 
https://cs.chromium.org/chromium/src/third_party/boringssl/src/crypto/fipsmodule/rand/rand.c?type=cs&sq=package:chromium&g=0

##### Misuse Case: Man in the middle (MitM)

As discussed here, there are some downgrade attacks that could potentially lead to MitM attacks:
https://www.chromium.org/Home/tls13
Code can be found here: 
https://cs.chromium.org/chromium/src/third_party/boringssl/src/ssl/tls13_server.cc

##### Code review Threat Model: 

###### CR List 
Chromium uses the concept of CRLSets (a curated list of revoked certificates) due to the performance impact of the growing list of revoked certificates.  
https://dev.chromium.org/Home/chromium-security/crlsets

This has been argued by some to be a weakness [1].

The CRLSet is used in the certificate verification code, some of which can be viewed here: 

https://cs.chromium.org/search/?q=crlset&type=cs

Here is where a certificate is verified: 

https://cs.chromium.org/chromium/src/net/socket/ssl_server_socket_impl.cc?type=cs&q=sslserversocketimpl&g=0&l=53


###### SSL Process / Server boundary 

From the threat model, it is important to point out the trust boundary between the server and the web browser.  This trust boundary is crossed in SSL mode by performing a TLS Handshake as shown here: 
https://cs.chromium.org/chromium/src/third_party/boringssl/src/ssl/handshake.cc?q=tls+handshake&dr=CSs

###### Extensions & Other Security Findings 
Another manual approach we conducted after a few of our automated tools, was to look into how the Chromium browser which is what our application is built on handles some of these race conditions and buffer overflow attacks. We looked at a few other code repositories to see if we could find any similar examples to [line 64](https://github.com/brave/brave-core/blob/master/browser/importer/chrome_profile_lock_unittest.cc) but weren’t able to. However, we came across a few [Chromium blog posts](https://chromereleases.googleblog.com/2019/03/stable-channel-update-for-desktop_12.html) that talk about the recent security updates/fixes they have conducted. 


*[$N/A][918861] Medium CVE-2019-5796: Race condition in Extensions. Reported by Mark Brand of Google Project Zero on 2019-01-03*

There was a race condition finding in the Chromium’s Extensions reported by a Google member which was recently fixed during the release. Here is the code snippet from that previous issue. 

 ``` c
 ExtensionsGuestViewMessageFilter::~ExtensionsGuestViewMessageFilter() {
  DCHECK_CURRENTLY_ON(BrowserThread::IO);
  // This map is created and accessed on the UI thread. Remove the reference to
  // |this| here so that it will not be accessed again; but leave erasing the
  // key from the global map to UI thread to avoid races when accessing the
  // underlying data structure (https:/ crbug.com/869791 ).
  (*GetProcessIdToFilterMap())[render_process_id_] = nullptr;
  base::PostTaskWithTraits(
      FROM_HERE, BrowserThread::UI,
      base::BindOnce(RemoveProcessIdFromGlobalMap, render_process_id_));
}
```
As you can see, this was an example of a race condition that existed in the Extensions code base. [For the full details on the bug finding.](https://bugs.chromium.org/p/chromium/issues/detail?id=918861) Other security findings that doesn’t apply much to the areas we were focusing on for our application, can be found [here.](https://chromereleases.googleblog.com/2019/11/stable-channel-update-for-desktop_18.html) This is just another representation of the mature and active community always working on improving and findings possible flaws to the Chromium code base. 


### Automated Code Scanning  
#### [Codacy](https://www.codacy.com/)

The first tool we used to analyze the Brave tool was Codacy. The tool was able to find 1086 total issues. The breakdown of these issues includes the following:

- Security = 27
- Error Prone = 16
- Code Style = 1043

Our team first began to look more into the large number we received back for the Code Style. When seeing this, our initial thoughts were that the “issues” flagged for this section would probably include a lot of “code grammar.” And after reviewing, it was in fact the case. For example, in the following path: “scripts/lint.py” the code picked up a few silly “issues.” 

<img width="668" alt="codacy-1" src="https://user-images.githubusercontent.com/45551925/69897430-9f86ba00-1311-11ea-89f5-f9661265a600.png">

Another “issue” we noticed during our automated testing was that during the following path: “lib/build.js” the code picked up an error for not using a semicolon. 

![issue2-SA](https://user-images.githubusercontent.com/45551925/70160691-861e9e80-1680-11ea-8c38-4e51d2f77b3b.png)

However, with JS it is best practice to use depends on the statement written since it doesn’t always need a semicolon to run, but it is best practice.  [Link to JS semicolon article](https://dev.to/adriennemiller/semicolons-in-javascript-to-use-or-not-to-use-2nli) 

Next, we began looking at our results at the issues noted for “Error Prone.” From our results we noticed that most of the issues for this contained information about the functions complexity. As this issues states, these issues are noted to emphasis on conducting a simplification on the line of code. For more information on how a user limiting complexity, see the [article here.](https://eslint.org/docs/rules/complexity) 

![issue3-SA](https://user-images.githubusercontent.com/45551925/70160782-aa7a7b00-1680-11ea-88c7-41e52e1df5cf.png)

Nevertheless, we then proceeded to review the security issues mentioned. The first security issue reported here was that many code lines contained a non literal argument at the index position of 0. 

More specifically, when looking at the first one: 

```js
const chromiumSrcDirLen = chromiumSrcDir.length
  sourceFiles.forEach(chromiumSrcFile => {
    var overriddenFile = path.join(config.srcDir, chromiumSrcFile.slice(chromiumSrcDirLen))
    if (!fs.existsSync(overriddenFile)) {
      // Try to check that original file is in gen dir.
      overriddenFile = path.join(config.outputDir, 'gen', chromiumSrcFile.slice(chromiumSrcDirLen))
```

[Line 28](https://github.com/brave/brave-browser/blob/master/lib/build.js) is what the tool highlighted that raised some security concerns. When looking into the [nodejs](https://nodejs.org/api/fs.html#fs_fs_existssync_path) documentation, this function takes in a path and will return true if it exists and false otherwise. But as you can see on [line 27](https://github.com/brave/brave-browser/blob/master/lib/build.js), the developers declare the variable used for the path that will be taking in. Thus, this was another security false positive that the tool warns when analyzing the repository. Other similar warnings can be seen in the Brave repository folder for [calculateFileChecksum.js](https://github.com/brave/brave-browser/blob/master/lib/calculateFileChecksum.js) as shown during the filestream filepath call; code example shown below.  


```js
module.exports = function CalculateFileChecksum(filePath, algorithm = 'sha256') {
  return new Promise((resolve, reject) => {
    try {
      const checksumGenerator = crypto.createHash(algorithm);
      const fileStream = fs.createReadStream(filePath)
      fileStream.on('error', function (err) {
        err.message = `CalculateFileChecksum error in FileStream at path "${filePath}": ${err.message}`
        reject(err)
      })
````
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/1f824366aa2b4609a521a94137ff0189)](https://www.codacy.com/manual/ramirezronald/brave-browser?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=ramirezronald/brave-browser&amp;utm_campaign=Badge_Grade) 
[Full Codacy Report](https://app.codacy.com/manual/ramirezronald/brave-browser/dashboard?bid=15417058)  

#### [Flawfinder](https://github.com/david-a-wheeler/flawfinder) 
Our group decided to also analyze some of the other repositories that make up the Brave application. Using Flawfinder mentioned from class, wanted to analyze a different repository to see what kind of results we would be able to find, so we looked at the [Brave Core Engine](https://github.com/brave/brave-core) which is 56.1% C++. Here are out results:

##### Total Hits/Issue = 87
##### Lines of code analyzed = 205648
##### Hits by Risk Level  

| Hits Level | Total Risk(s) |   
|---|---|
| 5 | 1  |  
| 4 | 11  |  
| 3 | 29 |   
| 2 | 41  |   
| 1 | 5  |  
| 0 | 0  |  


##### Findings based on Hits Level:

* Hits Risk Level  5
  * [CWE-362](https://cwe.mitre.org/data/definitions/362.html) 'Race Condition' & [CWE-20](https://cwe.mitre.org/data/definitions/20.html) 'Improper Input Validation'
  
* Hits Risk Level 4
    * [CWE-120](https://cwe.mitre.org/data/definitions/120.html) 'Classic Buffer Overflow'

* Hits Risk Level 3
    * [CWE-807](https://cwe.mitre.org/data/definitions/807.html) 'Reliance on Untrusted Inputs in a Security Decision'
    * [CWE-20](https://cwe.mitre.org/data/definitions/20.html) 'Improper Input Validation'
    * [CWE-327](https://cwe.mitre.org/data/definitions/327.html) 'Use of a Broken or Risky Cryptographic Algorithm'
    
* Hits Risk Level 2
    
    *  [CWE-119](https://cwe.mitre.org/data/definitions/119.html) 'Improper Restriction of Operations within the Bounds of a Memory Buffer'
    * [CWE-120](https://cwe.mitre.org/data/definitions/120.html) 'Classic Buffer Overflow'
    *  [CWE-362](https://cwe.mitre.org/data/definitions/362.html) 'Race Condition'

* Hits Risk Level 1
    * [CWE-126](https://cwe.mitre.org/data/definitions/126.html) 'Buffer Over-read'
    * [CWE-20](https://cwe.mitre.org/data/definitions/20.html) 'Improper Input Validation'
    *  [CWE-120](https://cwe.mitre.org/data/definitions/120.html) 'Classic Buffer Overflow'

Based on these results, we quickly focused on level 5 and 4 findings and began analyzing the improper input validation and race conditions noted by the tool. Looking at the [line 64](https://github.com/brave/brave-core/blob/master/browser/importer/chrome_profile_lock_unittest.cc) for the function "readlink" we looked to see how it was set up.

```c
#if defined(OS_POSIX)
  struct stat statbuf;
  if (expect) {
    ASSERT_EQ(0, lstat(lock_file_path_.value().c_str(), &statbuf));
    ASSERT_TRUE(S_ISLNK(statbuf.st_mode));
    char buf[PATH_MAX];
    ssize_t len = readlink(lock_file_path_.value().c_str(), buf, PATH_MAX);
    ASSERT_GT(len, 0);
  } else {
    ASSERT_GT(0, lstat(lock_file_path_.value().c_str(), &statbuf));
  }
  ```
From our brief experience with C, after looking at the the [documentation](http://man7.org/linux/man-pages/man2/readlink.2.html) for this function we came to the conclusion that it is setup properly. In this function, a symbolic link of the path will be placed in the buf which has a buf size set. If this wasn't the case, it could be an exploitable area for a malicious user to conduct a buffer overflow attack. 


[Full Flawfinder Report](https://github.com/jacob-barna/TripleJR/blob/master/AnalysisReports/SA-Flawfinder-Report.txt) 

Brave browser is based on Chrome, so the Chrome codebase was also scanned.  Note that the total number of hits only reflects those hits with severity 3+ as the report was too lengthy when all hits were included.

##### Total Hits/Issue = 4536 
##### Lines of code analyzed = 17676056
##### Hits by Risk Level  

| Hits Level | Total Risk(s) |   
|---|---|
| 5 | 101  |  
| 4 | 3612  |  
| 3 | 823 |   
| 2 | 11120  |   
| 1 | 4698  |  
| 0 | 13739  |  

##### Key Findings: 
SSL/TLS and crypto code are one of the most important features of the browser, and a key finding is that the automated scan found _no_ flaws (with severity level 3+) in the boringSSL library which implements TLS for Chrome/Brave-browser.

Because of the high number of hits, only those hits with the keyword crypto are examined below.  There are 19 hits related to crypto in the results.  Two of these hits are excluded from the stats below as they are in "SQLLite" unit tests and are not production code (and may in fact be intentional weaknesses).

Here are the breakdown of the remaining flaws by severity and their location in the code:

                                                     
| Source Location | Description (inferred from code) |        severity 3   |     severity 4     | severity 5 |
|---------|----------------------------------|---------------------|--------------------|------------|
|  /chrome/utils/importer/nss* | Import settings from Mozilla |         8         |          3         |      0     |
|  /chrome/components/gcm_driver/crypto/ | Google Cloud Messaging |         0         |          3         |      0     |
| /chrome/components/password_manager/core/browser/leak* | Password leak detection |         0         |          3         |      0   |

##### Importer
The warnings from the importer are all about weak encryption.  The schemes used are probably required to decrypt the Mozilla settings and are seemingly low risk.  

##### Google Cloud Messaging
Here are the hits for Google Cloud Messaging, all severity 4 and relating to:

*  [CWE-120](https://cwe.mitre.org/data/definitions/120.html) 'Classic Buffer Overflow'

•	[gcm_encryption_provider.cc](https://cs.chromium.org/chromium/src/components/gcm_driver/crypto/gcm_encryption_provider.cc?q=gcm_encryption_provider.cc&dr&l=404):404: [4] (buffer) StrCat: Does not check for buffer overflows when concatenating to destination [MS-banned] (CWE-120).
	  std::string payload = base::StrCat(
	  
•	[json_web_token_util.cc](https://cs.chromium.org/chromium/src/components/gcm_driver/crypto/json_web_token_util.cc?q=json_web_token&sq=package:chromium&g=0&l=59):59: [4] (buffer) StrCat: Does not check for buffer overflows when concatenating to destination [MS-banned] (CWE-120).
	  std::string data = base::StrCat({header_base64, ".", payload_base64});

•	[json_web_token_util.cc](https://cs.chromium.org/chromium/src/components/gcm_driver/crypto/json_web_token_util.cc?q=json_web_token&sq=package:chromium&g=0&l=79):79: [4] (buffer) StrCat: Does not check for buffer overflows when concatenating to destination [MS-banned] (CWE-120).
  return base::StrCat({data, ".", signature_base64});
	  
The code in question is the call to base::StrCat, such as this one from the gcm_encryption_provider.cc source file:
```c++
  std::string payload = base::StrCat(
      {salt, rs_str, key_length_str, sender_public_key, ciphertext});
```

It turns out that this is a custom "safe" strCat that automatically grows the size of the buffer using the [strAppendT](https://cs.chromium.org/chromium/src/base/strings/strcat.cc?dr&g=0&l=29) function, rendering these flaws as false positives:
```c++
template <typename DestString, typename InputString>
void StrAppendT(DestString* dest, span<const InputString> pieces) {
  size_t additional_size = 0;
  for (const auto& cur : pieces)
    additional_size += cur.size();
  ReserveAdditional(dest, additional_size);

  for (const auto& cur : pieces)
    dest->append(cur.data(), cur.size());
}
```


##### Browser Leak Detection

There are 3 reports of [CWE-120](https://cwe.mitre.org/data/definitions/120.html) "Classic Buffer Overflow," but these are all using the custom StrCat function as described above and are thusly also regarded as false positives in our analysis.

[Full Flawfinder Report (Chrome)](https://github.com/jacob-barna/TripleJR/blob/master/AnalysisReports/chrome_static_analysis.html)


#### [Flawfinder Results For Brave Tracking Protection](https://github.com/jacob-barna/TripleJR/blob/master/AnalysisReports/tracking-protection-flawfinder.txt) 
Using Flawfinder the [Brave Tracking Protection](https://github.com/brave/tracking-protection) was examined which is 83% C++. The results are as follows:

##### Total Hits/Issue = 82
##### Lines of code analyzed = 1251
##### Hits by Risk Level  

| Hits Level | Total Risk(s) |   
|---|---|
| 5 | 0 |  
| 4 | 15 |  
| 3 | 0 |   
| 2 | 18 |   
| 1 | 49 |  
| 0 | 0 |  

##### Findings based on Hits Level:

* Hits Risk Level 4
    * [CWE-120](https://cwe.mitre.org/data/definitions/120.html) 'Classic Buffer Overflow'

* Hits Risk Level 2
    * [CWE-119](https://cwe.mitre.org/data/definitions/119.html) 'Improper Restriction of Operations within the Bounds of a Memory Buffer'
    * [CWE-120](https://cwe.mitre.org/data/definitions/120.html) 'Classic Buffer Overflow'

* Hits Risk Level 1
    * [CWE-20](https://cwe.mitre.org/data/definitions/20.html) 'Improper Input Validation'
    * [CWE-120](https://cwe.mitre.org/data/definitions/120.html) 'Classic Buffer Overflow'
    * [CWE-126](https://cwe.mitre.org/data/definitions/126.html) 'Buffer Over-read'


#### [Flawfinder Results For Brave Ad-Block](https://github.com/jacob-barna/TripleJR/blob/master/AnalysisReports/ad-block-flawfinder.txt) 
Using Flawfinder the [Brave Ad-Block](https://github.com/brave/ad-block) was examined which is 42.9% C++. The results are as follows:

##### Total Hits/Issue = 125
##### Lines of code analyzed = 31468
##### Hits by Risk Level  

| Hits Level | Total Risk(s) |   
|---|---|
| 5 | 0 |  
| 4 | 2 |  
| 3 | 0 |   
| 2 | 56 |   
| 1 | 67 |  
| 0 | 0 |  

##### Findings based on Hits Level:

* Hits Risk Level 4
    * [CWE-134](https://cwe.mitre.org/data/definitions/134.html) 'Use of Externally-Controlled Format String'

* Hits Risk Level 2
    * [CWE-119](https://cwe.mitre.org/data/definitions/119.html) 'Improper Restriction of Operations within the Bounds of a Memory Buffer'
    * [CWE-120](https://cwe.mitre.org/data/definitions/120.html) 'Classic Buffer Overflow'
    * [CWE-362](https://cwe.mitre.org/data/definitions/362.html) 'Race Condition'

* Hits Risk Level 1
    * [CWE-126](https://cwe.mitre.org/data/definitions/126.html) 'Buffer Over-read'

##### Examination of results

Flawfinder detected two Level 4 risks inside the Ad-Block code [base.h](https://github.com/brave/ad-block/blob/master/base.h) file at lines 18 and 19 as follows:

```C++
#if defined(_MSC_VER) && _MSC_VER < 1900
#include <stdarg.h>
#include <stdio.h>
#define snprintf c99_snprintf
#define vsnprintf c99_vsnprintf
inline int c99_vsnprintf(char *outBuf, size_t size,
    const char *format, va_list ap) {
  int count = -1;
  if (size != 0) {
    count = _vsnprintf_s(outBuf, size, _TRUNCATE, format, ap);
  }
  if (count == -1) {
    count = _vscprintf(format, ap);
  }
  return count;
}
inline int c99_snprintf(char *outBuf, size_t size,
    const char *format, ...) {
  int count;
  va_list ap;
  va_start(ap, format);
  count = c99_vsnprintf(outBuf, size, format, ap);
  va_end(ap);
  return count;
}
#endif
```
Reviewing the [documentation](https://cwe.mitre.org/data/definitions/134.html) for CWE-134 it states "When an attacker can modify an externally-controlled format string, this can lead to buffer overflows, denial of service, or data representation problems." Researching more on snprintf (Write formatted output to sized buffer) and vsprintf (Write formatted data from variable argument list to sized buffer) it appears that these, when implemented properly, protect against buffer overflows as they limit the characters written. This is due to these functions outputted to a sized buffer. The implementation seems to be properly implemented and follows the required parameters to ensure the buffer size and formatting.

#### [MIR-SWAMP Results For Brave Tracking Protection](https://github.com/jacob-barna/TripleJR/blob/master/AnalysisReports/brave_tracking-protection.pdf) 
Using MIR-SWAMP the [Brave Tracking Protection](https://github.com/brave/tracking-protection) was examined for web scripting which is 8.6% JavaScript. The results are as follows:

<img width="838" alt="Screen Shot 2019-12-05 at 8 22 38 PM" src=https://user-images.githubusercontent.com/25576618/70290375-4f8a7600-179d-11ea-87df-4c270968a151.png>

##### Findings details:

* [CVE-2015-9251](https://nvd.nist.gov/vuln/detail/CVE-2015-9251)
    * Description: jQuery before 3.0.0 is vulnerable to Cross-site Scripting (XSS) attacks when a cross-domain Ajax request is performed without the dataType option, causing text/javascript responses to be executed.
    * Location: tracking-protection/node_modules/hashset-cpp/vendor/depot_tools/third_party/coverage/htmlfiles/jquery.min.js

* [CVE-2012-6708](https://nvd.nist.gov/vuln/detail/CVE-2012-6708)
    * Description: jQuery before 1.9.0 is vulnerable to Cross-site Scripting (XSS) attacks. The jQuery(strInput) function does not differentiate selectors from HTML in a reliable fashion. In vulnerable versions, jQuery determined whether the input was HTML by looking for the '<' character anywhere in the string, giving attackers more flexibility when attempting to construct a malicious payload. In fixed versions, jQuery only deems the input to be HTML if it explicitly starts with the '<' character, limiting exploitability only to attackers who can control the beginning of a string, which is far less common.
    * Location: tracking-protection/node_modules/hashset-cpp/vendor/depot_tools/third_party/coverage/htmlfiles/jquery.min.js

* [CVE-2011-4969](https://nvd.nist.gov/vuln/detail/CVE-2011-4969)
    * Description: Cross-site scripting (XSS) vulnerability in jQuery before 1.6.3, when using location.hash to select elements, allows remote attackers to inject arbitrary web script or HTML via a crafted tag.
    * Location: tracking-protection/node_modules/hashset-cpp/vendor/depot_tools/third_party/coverage/htmlfiles/jquery.min.js

* [CVE-2019-11358](https://nvd.nist.gov/vuln/detail/CVE-2019-11358)
    * Description: jQuery before 3.4.0, as used in Drupal, Backdrop CMS, and other products, mishandles jQuery.extend(true, {}, ...) because of Object.prototype pollution. If an unsanitized source object contained an enumerable __proto__ property, it could extend the native Object.prototype.
    * Location: tracking-protection/node_modules/hashset-cpp/vendor/depot_tools/third_party/coverage/htmlfiles/jquery.min.js


### Summary of Key Findings from Manual/Automated (Mappings to CWEs, CAPECs, Risk Levels, etc.) 

The assurance claim that Brave browser provides adequate confidentiality of communications when using SSL/TLS is evident in the code base.  By conducting manual analysis we found that TLS is implemented using a secure PRNG and robust encryption schemes.  We also find detailed documentation of the security concerns and mitigation in the project documentation.  Using the static analysis tool FlawFinder, we found many "hits" that are potential flaws.  The BoringSSL library triggered no "hits" which is reassuring.  In examining the flaws related to crypto implementations in ancillary packages (importer, cloud messaging, and password manager), we found that all of the "hits" were false positives as the open-source project uses custom implementations of commonly misused functions that prevent such misuse.  

Another key finding we noticed from conducting our automated and manual analysis was in regards to our first Flawfinder analysis. Since our Brave application is built on Chromium, our initial report mentioned a few risks that included the [CWE-362](https://cwe.mitre.org/data/definitions/362.html) ‘Race Condition’ & [CWE-120](https://cwe.mitre.org/data/definitions/120.html) ‘Classic Buffer Overflow.’ So what our team began doing was also looking at areas in the code base where this could be possible. However, as you can imagine, the popularity and maturity of this code base, makes it difficult to find any possible vulnerabilities to submit a report on. It was interesting to see that during this automated and manual approach, we were able to find security and bug fixes by google recently that included race condition flaws. This flaw was found in the Extensions code base which was a feature we were looking into throughout this semester; so maybe at an earlier time period, we could have been able to come across this and possible been able to contribute with any feedback. We also wanted to map our previous data flow for the Wallet feature during this approach but couldn’t find much since it is another 3rd party integration to our application. This is an area we really wanted to use automating tooling to see if any high risk security vulnerabilities could be found. Nevertheless, this was a challenging assignment due to some of our unfamiliarity with programming languages like C++ but it was fun. 

### Contribution To OSS

As stated above in the key findings, the Brave project is fairly large and has a lot of contributions from the OSS community. Due to the size, inexperience with C/C++, and being newer to in-depth code analysis our team looked at how Brave recommends users start off with contributions. On the [Brave Community Page](https://community.brave.com/) there is a thread for just that, titled [Contributing](https://community.brave.com/t/about-the-contributing-category/189). This thread outlines how the Brave community recommends users start off with contributing and who to contact regarding specific development areas.
For beginners, such as us, the community recommends that we first review all the threads and try to replicate issues that others have found. This would familiarize the user with the project along with learning what to look for and how to problem solve any issues found. For those with more experience the thread lists seasoned contributors to contact to get started with making recommendations and contributions to issues.

### Team Reflection
Initially, since this assignment was in between the Thanksgiving holiday, we didn’t have a whole lot of time to discuss in class together, but we are able to communicate everything we need through discord and GitHub. Our group was able to separate tasks individually to accomplish this assignment on time. Having the working session on 12/4 was also a lifesaver. A couple of our members from our team had some doubts as to what was expected or what to do with flaws found, but we were able to work with the team and receive feedback from the instructor to make sure we were on track. However, there were a few things that didn’t go well, such as not being too familiar with C++, a language many of us haven’t used in years. A couple of us on our team felt that we could contribute more to a JavaScript/TypeScript project, or C# (or at the very least Java) since that was something, we were more comfortable with. Regarding the online automated analysis tools, such as mir-swamp, a member from our team found it hard to try and get any of the C/C++ code for build and run. This resulted in finding other solutions such as testing for web scripting and running local tools like flawfinder on the C/C++ code. Overall, I think our groups great communication and teamwork really made it easier for us to accomplish these assignments. It was truly a pleasure to work with everyone on this team.  

[1]: https://www.grc.com/revocation/crlsets.htm

## Team GitHub 
[Team Repo](https://github.com/jacob-barna/TripleJR)  
[Team Project Board](https://github.com/jacob-barna/TripleJR/projects/5)  
