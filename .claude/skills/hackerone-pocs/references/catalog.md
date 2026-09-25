# HackerOne Disclosed-Report POC Catalog

Real, publicly disclosed HackerOne reports mirrored in this repo, grouped by weakness (CWE-style) category. **119 categories, 8670 report files.** Each category folder `weakness/<Category>/` holds one JSON per report plus a curated `index.md` (Title / URL / Severity / Reporter / Bounty).

Counts and up to 3 representative reports per category are listed below. Use these to find real-world examples of a vulnerability class, then open the category's `index.md` for the full list or the individual `<id>.json` for the write-up (`vulnerability_information` field).

## Category index (by report count)

| Reports | Category |
|--------:|----------|
| 1019 | Information Disclosure |
| 915 | Cross-site Scripting (XSS) - Generic |
| 723 | Violation of Secure Design Principles |
| 610 | Improper Authentication - Generic |
| 416 | Cross-Site Request Forgery (CSRF) |
| 415 | Cross-site Scripting (XSS) - Stored |
| 357 | Denial of Service |
| 324 | Cross-site Scripting (XSS) - Reflected |
| 320 | Privilege Escalation |
| 314 | Memory Corruption - Generic |
| 293 | Improper Access Control - Generic |
| 261 | Open Redirect |
| 226 | Code Injection |
| 198 | Business Logic Errors |
| 197 | SQL Injection |
| 186 | Command Injection - Generic |
| 169 | Insecure Direct Object Reference (IDOR) |
| 165 | Cryptographic Issues - Generic |
| 165 | Server-Side Request Forgery (SSRF) |
| 130 | Path Traversal |
| 119 | Cross-site Scripting (XSS) - DOM |
| 117 | UI Redressing (Clickjacking) |
| 60 | Brute Force |
| 48 | Privacy Violation |
| 36 | Buffer Over-read |
| 32 | OS Command Injection |
| 31 | CRLF Injection |
| 31 | Heap Overflow |
| 31 | Use After Free |
| 30 | Cleartext Storage of Sensitive Information |
| 30 | NULL Pointer Dereference |
| 29 | Information Exposure Through an Error Message |
| 28 | Classic Buffer Overflow |
| 28 | HTTP Request Smuggling |
| 27 | Deserialization of Untrusted Data |
| 26 | Out-of-bounds Read |
| 26 | XML External Entities (XXE) |
| 25 | Information Exposure Through Directory Listing |
| 24 | Improper Authorization |
| 24 | Insecure Storage of Sensitive Information |
| 24 | Phishing |
| 22 | Man-in-the-Middle |
| 21 | Insufficient Session Expiration |
| 20 | Improper Input Validation |
| 20 | Stack Overflow |
| 16 | Information Exposure Through Debug Information |
| 15 | Insufficiently Protected Credentials |
| 14 | Modification of Assumed-Immutable Data (MAID) |
| 13 | Cleartext Transmission of Sensitive Information |
| 13 | Improper Certificate Validation |
| 13 | Resource Injection |
| 12 | Remote File Inclusion |
| 11 | HTTP Response Splitting |
| 11 | Misconfiguration |
| 10 | Unrestricted Upload of File with Dangerous Type |
| 9 | Authentication Bypass Using an Alternate Path or Channel |
| 9 | Session Fixation |
| 8 | Array Index Underflow |
| 8 | Client-Side Enforcement of Server-Side Security |
| 8 | Use of Hard-coded Credentials |
| 7 | Forced Browsing |
| 7 | Improper Null Termination |
| 7 | Integer Overflow |
| 7 | Reliance on Cookies without Validation and Integrity Checking in a Security Decision |
| 7 | Time-of-check Time-of-use (TOCTOU) Race Condition |
| 7 | Weak Cryptography for Passwords |
| 7 | Weak Password Recovery Mechanism for Forgotten Password |
| 6 | Externally Controlled Reference to a Resource in Another Sphere |
| 6 | File and Directory Information Exposure |
| 6 | Plaintext Storage of a Password |
| 6 | Reliance on Untrusted Inputs in a Security Decision |
| 5 | Buffer Underflow |
| 5 | Double Free |
| 5 | Incorrect Authorization |
| 4 | Inadequate Encryption Strength |
| 4 | LDAP Injection |
| 4 | Malware |
| 4 | Password in Configuration File |
| 4 | Unverified Password Change |
| 4 | Use of a Broken or Risky Cryptographic Algorithm |
| 3 | Allocation of Resources Without Limits or Throttling |
| 3 | Improper Privilege Management |
| 3 | Information Exposure Through Sent Data |
| 3 | Integer Underflow |
| 3 | Missing Authentication for Critical Function |
| 3 | Missing Encryption of Sensitive Data |
| 3 | Missing Required Cryptographic Step |
| 3 | Security Through Obscurity |
| 3 | Type Confusion |
| 3 | Use of Cryptographically Weak Pseudo-Random Number Generator (PRNG) |
| 3 | Use of a Key Past its Expiration Date |
| 3 | User Interface (UI) Misrepresentation of Critical Information |
| 3 | Write-what-where Condition |
| 2 | Buffer Under-read |
| 2 | Execution with Unnecessary Privileges |
| 2 | Failure to Sanitize Special Elements into a Different Plane (Special Element Injection) |
| 2 | Improper Handling of Insufficient Permissions or Privileges |
| 2 | Improper Neutralization of HTTP Headers for Scripting Syntax |
| 2 | Incorrect Calculation of Buffer Size |
| 2 | Missing Authorization |
| 2 | Off-by-one Error |
| 2 | Use of Hard-coded Cryptographic Key |
| 2 | Use of Inherently Dangerous Function |
| 2 | XML Entity Expansion |
| 1 | Embedded Malicious Code |
| 1 | Exposed Dangerous Method or Function |
| 1 | Improper Check or Handling of Exceptional Conditions |
| 1 | Improper Export of Android Application Components |
| 1 | Improper Handling of URL Encoding (Hex Encoding) |
| 1 | Improper Neutralization of Escape, Meta, or Control Sequences |
| 1 | Improper Neutralization of Script-Related HTML Tags in a Web Page (Basic XSS) |
| 1 | Insecure Temporary File |
| 1 | Key Exchange without Entity Authentication |
| 1 | Reliance on Reverse DNS Resolution for a Security-Critical Action |
| 1 | Reusing a Nonce, Key Pair in Encryption |
| 1 | Unprotected Transport of Credentials |
| 1 | Use of Externally-Controlled Format String |
| 1 | Use of Hard-coded Password |
| 1 | XML Injection |

## Categories with representative reports

### Information Disclosure (1019 reports)
Folder: `weakness/Information Disclosure/` — full list in `index.md`.
- **Получение предложенных фотографий паблику**  
  https://hackerone.com/reports/227781 · bounty $200
- **Session Cookie Without Secure Flag,**  
  https://hackerone.com/reports/343095
- **Missing resource identifier encoding may lead to security vulnerabilities**  
  https://hackerone.com/reports/803922 · sev 4.8

### Cross-site Scripting (XSS) - Generic (915 reports)
Folder: `weakness/Cross-site Scripting (XSS) - Generic/` — full list in `index.md`.
- **Additonal stored XSS in Add note/Expected payment Date**  
  https://hackerone.com/reports/121903
- **Cross-site scripting (XSS) vulnerability on a DoD website**  
  https://hackerone.com/reports/186315
- **demo.owncloud.org: Web Server HTTP Trace/Track Method Support Cross-Site Tracing Vulnerability**  
  https://hackerone.com/reports/83837

### Violation of Secure Design Principles (723 reports)
Folder: `weakness/Violation of Secure Design Principles/` — full list in `index.md`.
- **Self-XSS in mails sent by hello@owncloud.com**  
  https://hackerone.com/reports/92111
- **IDOR - Ability to view unlisted products**  
  https://hackerone.com/reports/172545 · bounty $50
- **Login Hints on Admin Panel**  
  https://hackerone.com/reports/188195

### Improper Authentication - Generic (610 reports)
Folder: `weakness/Improper Authentication - Generic/` — full list in `index.md`.
- **Account Deleted without any confirmation**  
  https://hackerone.com/reports/42403
- **Default credentials on a DoD website**  
  https://hackerone.com/reports/192074
- **Top 10 2013-A2-Broken Authentication and Session Management - wordpress.com**  
  https://hackerone.com/reports/18503

### Cross-Site Request Forgery (CSRF) (416 reports)
Folder: `weakness/Cross-Site Request Forgery (CSRF)/` — full list in `index.md`.
- **Log Out Cross site Request Forgery**  
  https://hackerone.com/reports/7516
- **httponly flag not set + csrftoken in url**  
  https://hackerone.com/reports/188692
- **Отвязываем Twitter от любого профиля вк ! + несколько багов по дизайну**  
  https://hackerone.com/reports/71337 · bounty $250

### Cross-site Scripting (XSS) - Stored (415 reports)
Folder: `weakness/Cross-site Scripting (XSS) - Stored/` — full list in `index.md`.
- **Stored XXS @ https://steamcommunity.com/search/users/#text= via Profile Name**  
  https://hackerone.com/reports/351171 · sev 5.5 · bounty $750
- **Stored XSS on https://apps.topcoder.com/wiki/pages/editpage.action**  
  https://hackerone.com/reports/867133
- **Persistent XSS in Note objects**  
  https://hackerone.com/reports/508184 · bounty $4,500

### Denial of Service (357 reports)
Folder: `weakness/Denial of Service/` — full list in `index.md`.
- **Negative size in tar header causes infinite loop**  
  https://hackerone.com/reports/281336
- **Heap Buffer overflow in mrb_ary_unshift**  
  https://hackerone.com/reports/205521 · bounty $800
- **SIGSEGV - mrb_check_intern_str() - NullPointer**  
  https://hackerone.com/reports/193075 · bounty $800

### Cross-site Scripting (XSS) - Reflected (324 reports)
Folder: `weakness/Cross-site Scripting (XSS) - Reflected/` — full list in `index.md`.
- **[0.vk.com] Reflected XSS на странице подтверждения.**  
  https://hackerone.com/reports/502819 · bounty $200
- **Reflected XSS**  
  https://hackerone.com/reports/569241
- **A reflected XSS in python/Lib/DocXMLRPCServer.py**  
  https://hackerone.com/reports/705420 · sev 6.5 · bounty $500

### Privilege Escalation (320 reports)
Folder: `weakness/Privilege Escalation/` — full list in `index.md`.
- **Password Reset - query param overrides postdata**  
  https://hackerone.com/reports/96636 · bounty $1,500
- **Privilege Escalation using API->Feature**  
  https://hackerone.com/reports/239719 · sev 9.9 · bounty $1,500
- **Team member with Program permission only can escalate to Admin permission**  
  https://hackerone.com/reports/605720 · sev 4.8 · bounty $2,500

### Memory Corruption - Generic (314 reports)
Folder: `weakness/Memory Corruption - Generic/` — full list in `index.md`.
- **Adobe Flash Player ShimContentResolver.configure Memory Corruption Vulnerability**  
  https://hackerone.com/reports/145267 · bounty $2,000
- **integer overflow in preg_quote caused heap corruption**  
  https://hackerone.com/reports/167907 · bounty $500
- **NULL Pointer Dereference in WDDX Packet Deserialization with PDORow**  
  https://hackerone.com/reports/180908 · bounty $500

### Improper Access Control - Generic (293 reports)
Folder: `weakness/Improper Access Control - Generic/` — full list in `index.md`.
- **Access Projects And create projects in gitlab pre production server**  
  https://hackerone.com/reports/540711 · bounty $1,000
- **Possibility to overwrite any file in the vpe.cdn.vimeo.tv leads to the Stored XSS for the all customers on the embed.vhx.tv**  
  https://hackerone.com/reports/452559 · bounty $1,500
- **Initial mirror user can be assigned by other user even if the mirror was removed**  
  https://hackerone.com/reports/819821 · bounty $3,000

### Open Redirect (261 reports)
Folder: `weakness/Open Redirect/` — full list in `index.md`.
- **[crm.unikrn.com] Open Redirect**  
  https://hackerone.com/reports/297803 · bounty $50
- **Open Redirect possible in https://www.shopify.com/admin/**  
  https://hackerone.com/reports/161991 · bounty $500
- **Open redirection bypass .**  
  https://hackerone.com/reports/144525

### Code Injection (226 reports)
Folder: `weakness/Code Injection/` — full list in `index.md`.
- **Root Remote Code Execution on https://███**  
  https://hackerone.com/reports/632721
- **Java RMI (Remote Code Execution)**  
  https://hackerone.com/reports/163547
- **http://fitter1.i.mail.ru/browser/ торчит Graphite в мир**  
  https://hackerone.com/reports/60573 · bounty $400

### Business Logic Errors (198 reports)
Folder: `weakness/Business Logic Errors/` — full list in `index.md`.
- **REGISTRATION USING FAKE EMAIL ACCOUNT**  
  https://hackerone.com/reports/361941
- **H1514 Simple phishing using auto-created modal with weak URL-pattern check in incontext_app_link**  
  https://hackerone.com/reports/422279 · sev 5.4 · bounty $1,837
- **Missing link to TOTP manual enroll option**  
  https://hackerone.com/reports/249339 · bounty $90

### SQL Injection (197 reports)
Folder: `weakness/SQL Injection/` — full list in `index.md`.
- **Solr Injection in `user_id` parameter at :/v2/leaderboard_v2.json**  
  https://hackerone.com/reports/952501 · sev 9.1 · bounty $2,000
- **SQL Injection Vulnerability in Concrete5 version 5.7.3.1**  
  https://hackerone.com/reports/59664
- **[express-cart] Customer and admin email enumeration through MongoDB injection**  
  https://hackerone.com/reports/397445 · sev 8.2

### Command Injection - Generic (186 reports)
Folder: `weakness/Command Injection - Generic/` — full list in `index.md`.
- **CSV export filter bypass leads to formula injection.**  
  https://hackerone.com/reports/223999 · sev 5.4
- **[freespace] Command Injection due to Lack of Sanitization**  
  https://hackerone.com/reports/951249
- **Brave Browser unexpectedly allows to send arbitrary IPC messages**  
  https://hackerone.com/reports/187542 · bounty $300

### Insecure Direct Object Reference (IDOR) (169 reports)
Folder: `weakness/Insecure Direct Object Reference (IDOR)/` — full list in `index.md`.
- **IDOR редактирование любого вишлиста**  
  https://hackerone.com/reports/736065 · bounty $500
- **Authorization issue on 'valtakirjat' (/e2/verkkopalvelu/)**  
  https://hackerone.com/reports/307978 · sev 7.2 · bounty $490
- **Insecure Direct Object Reference on in-scope .mil website**  
  https://hackerone.com/reports/230026

### Cryptographic Issues - Generic (165 reports)
Folder: `weakness/Cryptographic Issues - Generic/` — full list in `index.md`.
- **Missing Certificate Authority Authorization rule**  
  https://hackerone.com/reports/410245
- **Security Missconfiguration in Autologin**  
  https://hackerone.com/reports/75936
- **Widespread failure of certificate validation in Android apps**  
  https://hackerone.com/reports/2293

### Server-Side Request Forgery (SSRF) (165 reports)
Folder: `weakness/Server-Side Request Forgery (SSRF)/` — full list in `index.md`.
- **SSRF in Exchange leads to ROOT access in all instances**  
  https://hackerone.com/reports/341876 · sev 6.9 · bounty $25,000
- **SSRF на https://target.my.com/**  
  https://hackerone.com/reports/200224 · sev 5.4 · bounty $800
- **SSRF in Export template to ActiveCampaign**  
  https://hackerone.com/reports/754025

### Path Traversal (130 reports)
Folder: `weakness/Path Traversal/` — full list in `index.md`.
- **[buttle] Path traversal in mid-buttle module allows to read any file in the server.**  
  https://hackerone.com/reports/358112 · sev 10
- **Чтение системных данных приложения: данные для авторизации, логи, БД, личная переписка**  
  https://hackerone.com/reports/373909 · sev 6.5 · bounty $150
- **[statics-server] Path Traversal due to lack of provided path sanitization**  
  https://hackerone.com/reports/355456

### Cross-site Scripting (XSS) - DOM (119 reports)
Folder: `weakness/Cross-site Scripting (XSS) - DOM/` — full list in `index.md`.
- **Inject page in admin panel via Shopify.API.pushState [New Payload]**  
  https://hackerone.com/reports/883867 · bounty $500
- **XSS on https://account.mail.ru/login via postMessage**  
  https://hackerone.com/reports/269349 · bounty $500
- **DOM-based Cross-Site Scripting in redirect url checkout**  
  https://hackerone.com/reports/299924

### UI Redressing (Clickjacking) (117 reports)
Folder: `weakness/UI Redressing (Clickjacking)/` — full list in `index.md`.
- **Registration bypass using OAuth logical bug**  
  https://hackerone.com/reports/64946 · bounty $40
- **X-Frame-Options**  
  https://hackerone.com/reports/237071
- **Clickjacking**  
  https://hackerone.com/reports/21110 · bounty $50

### Brute Force (60 reports)
Folder: `weakness/Brute Force/` — full list in `index.md`.
- **Insecure Direct Object Reference on in-scope .mil website**  
  https://hackerone.com/reports/230026
- **Rate limit missing at room login**  
  https://hackerone.com/reports/385381 · sev 4.3 · bounty $500
- **scripts loader DOS vulnerability**  
  https://hackerone.com/reports/690338

### Privacy Violation (48 reports)
Folder: `weakness/Privacy Violation/` — full list in `index.md`.
- **Получение чужого номера телефона (все цифры) через форму восстановления пароля**  
  https://hackerone.com/reports/350939 · bounty $300
- **Unauthorized Use of Victim Credit Card**  
  https://hackerone.com/reports/391385 · sev 3.5 · bounty $400
- **GetReports works for hubs you don't have access to**  
  https://hackerone.com/reports/350937 · sev 5 · bounty $750

### Buffer Over-read (36 reports)
Folder: `weakness/Buffer Over-read/` — full list in `index.md`.
- **CVE-2017-1000101: cURL: URL globbing out of bounds read**  
  https://hackerone.com/reports/255587 · sev 4.3
- **Multiple buffer over reads in mbox_from_parse**  
  https://hackerone.com/reports/836036 · sev 0 · bounty $50
- **ap_find_token() Buffer Overread**  
  https://hackerone.com/reports/241610 · sev 6.5 · bounty $1,500

### OS Command Injection (32 reports)
Folder: `weakness/OS Command Injection/` — full list in `index.md`.
- **RCE via ssh:// URIs in multiple VCS**  
  https://hackerone.com/reports/260005 · sev 8.8 · bounty $3,000
- **OS Command Execution on User's PC via CSV Injection**  
  https://hackerone.com/reports/282628
- **OS Command Injection in Nexus Repository Manager 2.x**  
  https://hackerone.com/reports/654888 · sev 9.1

### CRLF Injection (31 reports)
Folder: `weakness/CRLF Injection/` — full list in `index.md`.
- **CRLF Injection in 301 Redirect allow to Set-Cookies for mail.ru**  
  https://hackerone.com/reports/811366
- **CRLF injection in info.hacker.one**  
  https://hackerone.com/reports/217058
- **CRLF Injection [vpn.corp.cuvva.com]**  
  https://hackerone.com/reports/231508

### Heap Overflow (31 reports)
Folder: `weakness/Heap Overflow/` — full list in `index.md`.
- **Heap Overflow in fiber_switch triggered from Fiber.transfer**  
  https://hackerone.com/reports/227762 · bounty $100
- **Отсутствие flood контроля в ИСТОРИЯХ вк**  
  https://hackerone.com/reports/249786 · bounty $100
- **Heap memory can be accessible through metrics.solana.com**  
  https://hackerone.com/reports/962839

### Use After Free (31 reports)
Folder: `weakness/Use After Free/` — full list in `index.md`.
- **Old WebKit HTML agent in Template Preview function has multiple known vulnerabilities leading to RCE**  
  https://hackerone.com/reports/520717 · sev 9.8 · bounty $1,500
- **CVE-2017-10966: Heap-use-after-free in Irssi <1.0.4**  
  https://hackerone.com/reports/247028
- **Use After Free in unserialize()**  
  https://hackerone.com/reports/198732 · bounty $500

### Cleartext Storage of Sensitive Information (30 reports)
Folder: `weakness/Cleartext Storage of Sensitive Information/` — full list in `index.md`.
- **Sensitive information is publicly available**  
  https://hackerone.com/reports/282475 · sev 5
- **Access to Employee calendar disclosing internal presentation and meetings**  
  https://hackerone.com/reports/489284 · bounty $1,000
- **Insecure Storage and Overly Permissive  API Keys in Android App**  
  https://hackerone.com/reports/753868 · bounty $750

### NULL Pointer Dereference (30 reports)
Folder: `weakness/NULL Pointer Dereference/` — full list in `index.md`.
- **Null dereference in `cmd_denotify_operation_execute`**  
  https://hackerone.com/reports/965881 · bounty $50
- **Null dereference or redundant null check in `mail_crypt_load_global_private_key` for plugin mail-crypt**  
  https://hackerone.com/reports/908894 · sev 4.1 · bounty $50
- **SIGSEGV in mrb_str_inum**  
  https://hackerone.com/reports/217083 · bounty $800

### Information Exposure Through an Error Message (29 reports)
Folder: `weakness/Information Exposure Through an Error Message/` — full list in `index.md`.
- **Invalid Phabricator API token revealed through error message when escalating a report**  
  https://hackerone.com/reports/335123 · sev 0 · bounty $500
- **Tomcat examples available for public, Disclosure Apache Tomcat version, Critical/High/Medium CVE**  
  https://hackerone.com/reports/874427
- **lenta_proxy information disclosure**  
  https://hackerone.com/reports/890228 · sev 6.1 · bounty $400

### Classic Buffer Overflow (28 reports)
Folder: `weakness/Classic Buffer Overflow/` — full list in `index.md`.
- **Big XSS vulnerability!**  
  https://hackerone.com/reports/216330 · sev 6.9
- **PHP INI Parsing Stack Buffer Overflow Vulnerability**  
  https://hackerone.com/reports/248601 · sev 6.8 · bounty $500
- **Malformed BSP in GoldSrc Engine may cause shellcode injection**  
  https://hackerone.com/reports/458929 · bounty $1,750

### HTTP Request Smuggling (28 reports)
Folder: `weakness/HTTP Request Smuggling/` — full list in `index.md`.
- **Unauthenticated request smuggling on launchpad.37signals.com**  
  https://hackerone.com/reports/867577 · bounty $1,737
- **HTTP Header Injection/HTTP_Response_Splitting**  
  https://hackerone.com/reports/214436
- **Password theft login.newrelic.com via Request Smuggling**  
  https://hackerone.com/reports/498052 · bounty $3,000

### Deserialization of Untrusted Data (27 reports)
Folder: `weakness/Deserialization of Untrusted Data/` — full list in `index.md`.
- **Remote Code Execution through Deserialization Attack in OwnBackup app.**  
  https://hackerone.com/reports/562335
- **Deserialization of Untrusted Data in www/delivery/dxmlrpc.php**  
  https://hackerone.com/reports/542670 · sev 10
- **Remote Code Execution (RCE) in a Sony Pictures WebSystem**  
  https://hackerone.com/reports/330028 · sev 10

### Out-of-bounds Read (26 reports)
Folder: `weakness/Out-of-bounds Read/` — full list in `index.md`.
- **`put` allocates uninitialized Buffers when non-round numbers are passed in input**  
  https://hackerone.com/reports/321702 · sev 1.8
- **`byte` allocates uninitialized buffers and reads data from them past the initialized length**  
  https://hackerone.com/reports/330351 · sev 5.2
- **`stringstream` allocates uninitialized Buffers when number is passed in input stream on Node.js 4.x and below**  
  https://hackerone.com/reports/321670 · sev 5.2

### XML External Entities (XXE) (26 reports)
Folder: `weakness/XML External Entities (XXE)/` — full list in `index.md`.
- **XXE in DoD website that may lead to RCE**  
  https://hackerone.com/reports/227880
- **Uploaded XLF files result in External Entity Execution**  
  https://hackerone.com/reports/232614 · sev 7.1
- **XXE on sms-be-vip.twitter.com in SXMP Processor**  
  https://hackerone.com/reports/248668 · sev 5.3 · bounty $10,080

### Information Exposure Through Directory Listing (25 reports)
Folder: `weakness/Information Exposure Through Directory Listing/` — full list in `index.md`.
- **Information Exposure Through Directory Listing**  
  https://hackerone.com/reports/260221
- **Upload directory of Mtn.ci**  
  https://hackerone.com/reports/762118 · sev 5.3
- **[serve] Directory listing and File access even when they have been set to be ignored**  
  https://hackerone.com/reports/330650 · sev 9.3

### Improper Authorization (24 reports)
Folder: `weakness/Improper Authorization/` — full list in `index.md`.
- **Shopify admin authentication bypass using partners.shopify.com**  
  https://hackerone.com/reports/270981 · sev 10 · bounty $20,000
- **Account Takeover via billing**  
  https://hackerone.com/reports/394329 · sev 9.1 · bounty $8,000
- **Improper Authorization at https://api-my.pay.razer.com/v1/trxDetail?trxId=[Id] allowing unauthorised access to other user's transaction details**  
  https://hackerone.com/reports/754339 · sev 6.5 · bounty $500

### Insecure Storage of Sensitive Information (24 reports)
Folder: `weakness/Insecure Storage of Sensitive Information/` — full list in `index.md`.
- **Access Projects And create projects in gitlab pre production server**  
  https://hackerone.com/reports/540711 · bounty $1,000
- **SSN leak due to editable slides**  
  https://hackerone.com/reports/693943
- **PII Leak (such as CAC User ID) at https://████████/pages/login.aspx**  
  https://hackerone.com/reports/900137

### Phishing (24 reports)
Folder: `weakness/Phishing/` — full list in `index.md`.
- **Email Spoofing**  
  https://hackerone.com/reports/793532
- **Missing URL sanitization in comments can be leveraged for phishing**  
  https://hackerone.com/reports/252894
- **Content injection on shared event (calendar.mail.ru)**  
  https://hackerone.com/reports/847473 · bounty $150

### Man-in-the-Middle (22 reports)
Folder: `weakness/Man-in-the-Middle/` — full list in `index.md`.
- **Domain does not Match SSL Certificate**  
  https://hackerone.com/reports/504507
- **http://lists.parrotsec.org vulnerable to MITM**  
  https://hackerone.com/reports/238344
- **XSS on account.mail.ru/login**  
  https://hackerone.com/reports/291522 · bounty $500

### Insufficient Session Expiration (21 reports)
Folder: `weakness/Insufficient Session Expiration/` — full list in `index.md`.
- **The Microsoft Store Uber App Does Not Implement Server-side Token Revocation**  
  https://hackerone.com/reports/293363
- **No Session change on Password change**  
  https://hackerone.com/reports/280585
- **No expiration of session ID after Password change**  
  https://hackerone.com/reports/223327

### Improper Input Validation (20 reports)
Folder: `weakness/Improper Input Validation/` — full list in `index.md`.
- **Improper UUID validation results in bypass of #419896**  
  https://hackerone.com/reports/423073 · sev 7.7 · bounty $7,500
- **Bug in OAuth Success Redirect URI Validation**  
  https://hackerone.com/reports/753547
- **HTTP header values do not have trailing OWS trimmed**  
  https://hackerone.com/reports/730779 · sev 7.4 · bounty $250

### Stack Overflow (20 reports)
Folder: `weakness/Stack Overflow/` — full list in `index.md`.
- **VLC 4.0.0 - Stack Buffer Overflow (SEH)**  
  https://hackerone.com/reports/489102 · bounty $2,817.28
- **Stack overflow affecting "ext" field on stylers.xml configuration file**  
  https://hackerone.com/reports/480984 · sev 6.8 · bounty $1,144.89
- **Perl $ENV Key Stack Buffer Overflow**  
  https://hackerone.com/reports/272497 · bounty $1,500

### Information Exposure Through Debug Information (16 reports)
Folder: `weakness/Information Exposure Through Debug Information/` — full list in `index.md`.
- **Apache mod_status /server-status Information Disclosure**  
  https://hackerone.com/reports/541347 · sev 5.3
- **ms5 debug page exposing internal info (internal IPs, headers)**  
  https://hackerone.com/reports/311326 · bounty $280
- **404-response contains debug-information with all headers**  
  https://hackerone.com/reports/792998 · bounty $500

### Insufficiently Protected Credentials (15 reports)
Folder: `weakness/Insufficiently Protected Credentials/` — full list in `index.md`.
- **Sensitive Information Leaking Through DARPA Website. [█████████]**  
  https://hackerone.com/reports/805027
- **Admin Salt Leakage on DoD site.**  
  https://hackerone.com/reports/241116
- **Possible Subdomain Takeover**  
  https://hackerone.com/reports/233402

### Modification of Assumed-Immutable Data (MAID) (14 reports)
Folder: `weakness/Modification of Assumed-Immutable Data (MAID)/` — full list in `index.md`.
- **Prototype pollution in dot-prop**  
  https://hackerone.com/reports/719856 · sev 6.3
- **[supermixer] Prototype pollution**  
  https://hackerone.com/reports/959987
- **[nested-property] Prototype Pollution**  
  https://hackerone.com/reports/788883 · sev 5.9

### Cleartext Transmission of Sensitive Information (13 reports)
Folder: `weakness/Cleartext Transmission of Sensitive Information/` — full list in `index.md`.
- **Missing SSL can leak job token**  
  https://hackerone.com/reports/222036
- **Accessing to download.nextcloud.com from original ip adreess | insecure Download**  
  https://hackerone.com/reports/374053
- **Login form on non-HTTPS page on http://stream.highwebmedia.com/auth/login/**  
  https://hackerone.com/reports/386735 · bounty $100

### Improper Certificate Validation (13 reports)
Folder: `weakness/Improper Certificate Validation/` — full list in `index.md`.
- **Social App does not validate server certificates for outgoing connections**  
  https://hackerone.com/reports/915585 · sev 5.4
- **Insecure HostnameVerifier within WebView of Razer Pay Android (TLS Vulnerability)**  
  https://hackerone.com/reports/795272 · bounty $750
- **Incorrect HTTPS Certificate**  
  https://hackerone.com/reports/225540

### Resource Injection (13 reports)
Folder: `weakness/Resource Injection/` — full list in `index.md`.
- **Arbitrary local system file read on open-xchange server**  
  https://hackerone.com/reports/303744 · sev 10 · bounty $2,000
- **HTML Injection in Owncloud**  
  https://hackerone.com/reports/215410 · sev 5.4 · bounty $150
- **CSS Injection on static.mackeeper.com - Potential XSS**  
  https://hackerone.com/reports/783993 · sev 3.6 · bounty $50

### Remote File Inclusion (12 reports)
Folder: `weakness/Remote File Inclusion/` — full list in `index.md`.
- **Remote file inclusion using "/cdn-cgi/pe/bag2?r[]="**  
  https://hackerone.com/reports/346575
- **Keybase client (Windows 10): Write files anywhere in userland using relative path in "download attachement" feature**  
  https://hackerone.com/reports/713006 · sev 7.6 · bounty $5,000
- **SSRF & LFR via on city-mobil.ru**  
  https://hackerone.com/reports/748123 · sev 8.3 · bounty $6,000

### HTTP Response Splitting (11 reports)
Folder: `weakness/HTTP Response Splitting/` — full list in `index.md`.
- **CRLF инъекция на https://tz.mail.ru**  
  https://hackerone.com/reports/205796
- **[newscdn.starbucks.com] CRLF Injection, XSS**  
  https://hackerone.com/reports/192749
- **HTTP Host Header Injection on app.goodhire.com**  
  https://hackerone.com/reports/277354

### Misconfiguration (11 reports)
Folder: `weakness/Misconfiguration/` — full list in `index.md`.
- **Bypass front server restrictions and access to forbidden files and directories through X-Rewrite-Url/X-original-url header on account.mackeeper.com**  
  https://hackerone.com/reports/737323 · sev 6.1 · bounty $300
- **Django DEBUG mode enabled and leaked system information.**  
  https://hackerone.com/reports/963542
- **Mirror of https://city-mobil.ru admin interface**  
  https://hackerone.com/reports/749677 · bounty $150

### Unrestricted Upload of File with Dangerous Type (10 reports)
Folder: `weakness/Unrestricted Upload of File with Dangerous Type/` — full list in `index.md`.
- **Unrestricted File Upload on https://app.dropcontact.io/app/upload/**  
  https://hackerone.com/reports/949295
- **Unrestricted File Upload on https://my.stripo.email and https://stripo.email**  
  https://hackerone.com/reports/823588
- **Unrestricted file upload when creating quotes allows for Stored XSS**  
  https://hackerone.com/reports/788397 · sev 5.2 · bounty $250

### Authentication Bypass Using an Alternate Path or Channel (9 reports)
Folder: `weakness/Authentication Bypass Using an Alternate Path or Channel/` — full list in `index.md`.
- **Two-factor authentication (2FA) Bypass**  
  https://hackerone.com/reports/708303
- **SDC bypass on calendar.mail.ru**  
  https://hackerone.com/reports/1024029 · sev 4.8 · bounty $1,500
- **Admin panel take over | User info leakage | Mass Comprimise**  
  https://hackerone.com/reports/428757

### Session Fixation (9 reports)
Folder: `weakness/Session Fixation/` — full list in `index.md`.
- **Password Reset page Session Fixation**  
  https://hackerone.com/reports/255020
- **Affiliates - Session Fixation**  
  https://hackerone.com/reports/737058
- **H1514 Session Fixation on multiple shopify-built apps on *.shopifycloud.com and *.shopifyapps.com**  
  https://hackerone.com/reports/423136 · bounty $5,000

### Array Index Underflow (8 reports)
Folder: `weakness/Array Index Underflow/` — full list in `index.md`.
- **https://publishers.basicattentiontoken.org/favicon.ico is Vulnerable to CVE-2017-7529**  
  https://hackerone.com/reports/980856 · sev 5.2 · bounty $100
- **memory corruption while parsing HTTP response**  
  https://hackerone.com/reports/320222 · bounty $500
- **Unchecked weapon id in WeaponList message parser on client leads to RCE**  
  https://hackerone.com/reports/513154 · sev 9.8 · bounty $3,000

### Client-Side Enforcement of Server-Side Security (8 reports)
Folder: `weakness/Client-Side Enforcement of Server-Side Security/` — full list in `index.md`.
- **User is able to access and create private synthetics locations without upgrading (regression of #276157)**  
  https://hackerone.com/reports/344468 · bounty $500
- **Giving myself access to NR1 UI / one.newrelic.com without the proper feature flags on my account**  
  https://hackerone.com/reports/520623 · bounty $500
- **File Upload Restriction Bypass**  
  https://hackerone.com/reports/259913

### Use of Hard-coded Credentials (8 reports)
Folder: `weakness/Use of Hard-coded Credentials/` — full list in `index.md`.
- **API Keys Hardcoded in Github repository**  
  https://hackerone.com/reports/766346
- **[com.smule.autorap.*] Cloud Messaging/Push Notification service takeover due to clear-text usage of Legacy FCM Server keys in the client app**  
  https://hackerone.com/reports/789370
- **Hard coded Username and password in GiHub commit**  
  https://hackerone.com/reports/877402

### Forced Browsing (7 reports)
Folder: `weakness/Forced Browsing/` — full list in `index.md`.
- **[Android org.torproject.android] Possible to force list of bridges**  
  https://hackerone.com/reports/252626
- **Potential server misconfiguration leads to disclosure of vendor/ directory**  
  https://hackerone.com/reports/271391
- **403 Forbidden Bypass at www.██████.mil**  
  https://hackerone.com/reports/991717

### Improper Null Termination (7 reports)
Folder: `weakness/Improper Null Termination/` — full list in `index.md`.
- **DirectoryIterator class silently truncates after a null byte**  
  https://hackerone.com/reports/805013 · bounty $500
- **Null Byte Injection in all fields of Profile**  
  https://hackerone.com/reports/255125
- **Cache poisoning using NULL bytes and long URLs**  
  https://hackerone.com/reports/334709 · sev 5.8 · bounty $500

### Integer Overflow (7 reports)
Folder: `weakness/Integer Overflow/` — full list in `index.md`.
- **Unsafe arithmetic in PyString_DecodeEscape**  
  https://hackerone.com/reports/241202 · bounty $500
- **Int Overflow lead to Heap OverFlow in exif_thumbnail_extract of exif.c**  
  https://hackerone.com/reports/384477 · sev 5.3 · bounty $500
- **Signed integer overflow in tool_progress_cb()**  
  https://hackerone.com/reports/591770

### Reliance on Cookies without Validation and Integrity Checking in a Security Decision (7 reports)
Folder: `weakness/Reliance on Cookies without Validation and Integrity Checking in a Security Decision/` — full list in `index.md`.
- **Cookie injection leads to complete DoS over whole domain *.mackeeper.com. Injection point accountstage.mackeeper.com/**  
  https://hackerone.com/reports/861521 · bounty $50
- **Отправка писем с произвольным текстом/кликабельными ссылками любому зарегистрированному пользователю с указанной почтой, зная только steamid**  
  https://hackerone.com/reports/993711 · sev 9.7 · bounty $2,000
- **Rack parses encoded cookie names allowing an attacker to send malicious `__Host-` and `__Secure-` prefixed cookies**  
  https://hackerone.com/reports/895727

### Time-of-check Time-of-use (TOCTOU) Race Condition (7 reports)
Folder: `weakness/Time-of-check Time-of-use (TOCTOU) Race Condition/` — full list in `index.md`.
- **Ability to bypass partner email confirmation to take over any store given an employee email**  
  https://hackerone.com/reports/300305 · sev 10 · bounty $15,250
- **Race condition in claiming program credentials**  
  https://hackerone.com/reports/488985 · sev 3.4 · bounty $500
- **Race Condition leads to undeletable group member**  
  https://hackerone.com/reports/604534 · sev 2.4 · bounty $500

### Weak Cryptography for Passwords (7 reports)
Folder: `weakness/Weak Cryptography for Passwords/` — full list in `index.md`.
- **Setting a password with a single character**  
  https://hackerone.com/reports/223851
- **Weak password**  
  https://hackerone.com/reports/267539
- **Weak Cryptography for Passwords**  
  https://hackerone.com/reports/260689

### Weak Password Recovery Mechanism for Forgotten Password (7 reports)
Folder: `weakness/Weak Password Recovery Mechanism for Forgotten Password/` — full list in `index.md`.
- **Week Passwords generated by password reset function**  
  https://hackerone.com/reports/765031
- **(Possible) staff account takeover via reset token bruteforce at helpdesk.bistudio.com**  
  https://hackerone.com/reports/332632 · bounty $200
- **Reset password without knowing current password**  
  https://hackerone.com/reports/806055

### Externally Controlled Reference to a Resource in Another Sphere (6 reports)
Folder: `weakness/Externally Controlled Reference to a Resource in Another Sphere/` — full list in `index.md`.
- **molotok.m.mail.ru delegated to external entity**  
  https://hackerone.com/reports/376808 · bounty $1,500
- **Subdomain Takeover at blog.instamart.ru**  
  https://hackerone.com/reports/894431 · sev 3.8
- **Reference to external uncontrolled resource in terrhq.ru**  
  https://hackerone.com/reports/430254

### File and Directory Information Exposure (6 reports)
Folder: `weakness/File and Directory Information Exposure/` — full list in `index.md`.
- **Internal Path Disclosure**  
  https://hackerone.com/reports/979110 · bounty $100
- **Открытый .htaccess на cookery.zakazaka.ru**  
  https://hackerone.com/reports/596368 · sev 0
- **Open FTP server on a DoD system**  
  https://hackerone.com/reports/192321

### Plaintext Storage of a Password (6 reports)
Folder: `weakness/Plaintext Storage of a Password/` — full list in `index.md`.
- **Nextcloud logs ldap passwords**  
  https://hackerone.com/reports/264426
- **Password of failed (2FA) login attempt is stored in log**  
  https://hackerone.com/reports/244092
- **Github test clientID and clientSecret leaked**  
  https://hackerone.com/reports/796139

### Reliance on Untrusted Inputs in a Security Decision (6 reports)
Folder: `weakness/Reliance on Untrusted Inputs in a Security Decision/` — full list in `index.md`.
- **Helpdesk Takeover at dmc.datastax.com**  
  https://hackerone.com/reports/759454 · sev 8.3 · bounty $1,000
- **Bypass Email Verification -- Able to Access Internal Gitlab Services that use Login with Gitlab and Perform Check on email domain**  
  https://hackerone.com/reports/565883 · bounty $3,000
- **[authdl.mail.ru] Spoofing IP address**  
  https://hackerone.com/reports/549130 · sev 0 · bounty $250

### Buffer Underflow (5 reports)
Folder: `weakness/Buffer Underflow/` — full list in `index.md`.
- **[H1-2006 2020]  Got the flag**  
  https://hackerone.com/reports/887744
- **[CVE-2018-6913] heap-buffer-overflow in S_pack_rec**  
  https://hackerone.com/reports/354650 · bounty $1,000
- **CVE-2019-11043: a buffer underflow in fpm_main.c can lead to RCE in php-fpm**  
  https://hackerone.com/reports/722327 · bounty $1,500

### Double Free (5 reports)
Folder: `weakness/Double Free/` — full list in `index.md`.
- **Access Violation Reading EXPLOITABLE_0228**  
  https://hackerone.com/reports/503208 · bounty $1,135.32
- **krb5: double-free in read_data() after realloc() fail**  
  https://hackerone.com/reports/686823 · sev 6.3 · bounty $200
- **SIGABRT - mirb - Double Free**  
  https://hackerone.com/reports/214576 · bounty $100

### Incorrect Authorization (5 reports)
Folder: `weakness/Incorrect Authorization/` — full list in `index.md`.
- **Email verification bypasa**  
  https://hackerone.com/reports/763458
- **OTP bypass - Unintended disclosure of OTP to client allows attacker to manage users' subscriptions**  
  https://hackerone.com/reports/777957 · sev 6.3
- **A user can request a report to be retested even though the program has not been verified by HackerOne**  
  https://hackerone.com/reports/448078 · sev 3.8 · bounty $500

### Inadequate Encryption Strength (4 reports)
Folder: `weakness/Inadequate Encryption Strength/` — full list in `index.md`.
- **Insufficient DKIM record with RSA 512-bit key used on WordPress.com**  
  https://hackerone.com/reports/550937 · sev 4.2 · bounty $250
- **RC4 cipher suit in use in vpn.corp.cuvva.co**  
  https://hackerone.com/reports/231068
- **[smena.samokat.ru] Predictable JWT secret**  
  https://hackerone.com/reports/896649 · sev 7.2 · bounty $400

### LDAP Injection (4 reports)
Folder: `weakness/LDAP Injection/` — full list in `index.md`.
- **Information disclosure on a DoD website**  
  https://hackerone.com/reports/184076
- **[cloudron-surfer] Denial of Service via LDAP Injection**  
  https://hackerone.com/reports/906959
- **[meemo-app] Denial of Service via LDAP Injection**  
  https://hackerone.com/reports/907311

### Malware (4 reports)
Folder: `weakness/Malware/` — full list in `index.md`.
- **Vulnerability in GoldSource Engine allows to upload and run an arbitrary DLL on client**  
  https://hackerone.com/reports/508894 · bounty $1,000
- **Tricking the "Create snippet" feature into displaying the wrong filetype can lead to RCE on Slack users**  
  https://hackerone.com/reports/833080 · sev 8.7 · bounty $1,500
- **Trojan:JS/CoinMiner in npm files**  
  https://hackerone.com/reports/687325

### Password in Configuration File (4 reports)
Folder: `weakness/Password in Configuration File/` — full list in `index.md`.
- **MySQL username and password leaked on [2017.russianaicup.ru]**  
  https://hackerone.com/reports/879389 · sev 6.1 · bounty $150
- **MySQL username and password leaked in developer.valvesoftware.com via source code dislosure**  
  https://hackerone.com/reports/291057 · bounty $1,000
- **Insecure Zendesk SSO implementation by generating JWT client-side**  
  https://hackerone.com/reports/638635 · sev 8.1

### Unverified Password Change (4 reports)
Folder: `weakness/Unverified Password Change/` — full list in `index.md`.
- **Monero wallet password change is confirmed when not matching**  
  https://hackerone.com/reports/803028
- **暴力破解用户密码没有速率控制**  
  https://hackerone.com/reports/854424 · bounty $700
- **Password Change not notified when changed from settings**  
  https://hackerone.com/reports/242846

### Use of a Broken or Risky Cryptographic Algorithm (4 reports)
Folder: `weakness/Use of a Broken or Risky Cryptographic Algorithm/` — full list in `index.md`.
- **SSH server compatible with several vulnerable cryptographic algorithms**  
  https://hackerone.com/reports/318068 · bounty $300
- **HTTPS is not validating TLS mac codes**  
  https://hackerone.com/reports/402671
- **License verification mechanism can be bypassed**  
  https://hackerone.com/reports/411068

### Allocation of Resources Without Limits or Throttling (3 reports)
Folder: `weakness/Allocation of Resources Without Limits or Throttling/` — full list in `index.md`.
- **i don't the important and it's impact  . the affected asset : https://github.com/solana-labs/solana/blob/master/.buildkite/env/secrets.ejson**  
  https://hackerone.com/reports/961167
- **i don't the important and it's impact . the affected asset: https://github.com/solana-labs/solana/blob/master/.buildkite/env/secrets.ejson**  
  https://hackerone.com/reports/961175 · sev 5.8
- **Prototype pollution attack (lodash)**  
  https://hackerone.com/reports/712065 · sev 7.4 · bounty $250

### Improper Privilege Management (3 reports)
Folder: `weakness/Improper Privilege Management/` — full list in `index.md`.
- **Unauthenticated access to sensitive user information**  
  https://hackerone.com/reports/702677 · sev 5.4 · bounty $500
- **[H1-2006 2020] Exploiting multiple vulnerabilities to get hacker's payment ensured**  
  https://hackerone.com/reports/894949
- **Re-Sharing allows increase of privileges**  
  https://hackerone.com/reports/889243 · sev 5.5 · bounty $750

### Information Exposure Through Sent Data (3 reports)
Folder: `weakness/Information Exposure Through Sent Data/` — full list in `index.md`.
- **Google Maps API key leaked during device pairing**  
  https://hackerone.com/reports/724039 · sev 4.9 · bounty $150
- **IDOR on mcs.mail.ru**  
  https://hackerone.com/reports/312555 · bounty $150
- **Leaking Username and Password in the URLs via Virustotal, can leads to account takeover**  
  https://hackerone.com/reports/411920

### Integer Underflow (3 reports)
Folder: `weakness/Integer Underflow/` — full list in `index.md`.
- **Access Violation Reading in libfaad_plugin**  
  https://hackerone.com/reports/502816 · bounty $1,120.81
- **Integer Underflow @ ossl_cipher_pkcs5_keyivgen**  
  https://hackerone.com/reports/304115
- **Interger overflow in eval trigger write out of bound**  
  https://hackerone.com/reports/272097

### Missing Authentication for Critical Function (3 reports)
Folder: `weakness/Missing Authentication for Critical Function/` — full list in `index.md`.
- **Token leak in security challenge flow allows retrieving victim's PayPal email and plain text password**  
  https://hackerone.com/reports/739737 · sev 8 · bounty $15,300
- **Administration page visible without authentication**  
  https://hackerone.com/reports/809357 · bounty $100
- **[c-api.city-mobil.ru] Client authentication bypass leads to information disclosure**  
  https://hackerone.com/reports/772118 · sev 9.7 · bounty $8,000

### Missing Encryption of Sensitive Data (3 reports)
Folder: `weakness/Missing Encryption of Sensitive Data/` — full list in `index.md`.
- **Yarn transfers npm credentials over unencrypted http connection**  
  https://hackerone.com/reports/640904 · sev 8.2
- **Cloudflare does not sufficiently truncate credit card numbers in invoices**  
  https://hackerone.com/reports/293276
- **ChaCha20-Poly1305 with long nonces**  
  https://hackerone.com/reports/506040 · sev 7.4 · bounty $500

### Missing Required Cryptographic Step (3 reports)
Folder: `weakness/Missing Required Cryptographic Step/` — full list in `index.md`.
- **Constant-time comparison is not always implemented; critical areas are vulnerable to key-timing attacks**  
  https://hackerone.com/reports/363680
- **Phabricator is vulnerable to padding oracle attacks and chosen-ciphertext attacks.**  
  https://hackerone.com/reports/216746 · sev 5.3 · bounty $750
- **Fedora installation instructions fetch repo and validation key from insecure source, allowing mitm attack**  
  https://hackerone.com/reports/638250 · bounty $216

### Security Through Obscurity (3 reports)
Folder: `weakness/Security Through Obscurity/` — full list in `index.md`.
- **Safe Redirect Bypass**  
  https://hackerone.com/reports/945990 · bounty $560
- **All Burp Suite Scan report**  
  https://hackerone.com/reports/513172
- **[h1-415 2020] H1-415 CTF Writeup by W--**  
  https://hackerone.com/reports/780285

### Type Confusion (3 reports)
Folder: `weakness/Type Confusion/` — full list in `index.md`.
- **User provided values passed to PHP unset() function**  
  https://hackerone.com/reports/292500
- **Type Confusion in Object Deserialization**  
  https://hackerone.com/reports/198733 · bounty $500
- **Insufficient Type Check leading to Developer ability to delete Project, Repository, Group, ...**  
  https://hackerone.com/reports/960244 · bounty $5,000

### Use of Cryptographically Weak Pseudo-Random Number Generator (PRNG) (3 reports)
Folder: `weakness/Use of Cryptographically Weak Pseudo-Random Number Generator (PRNG)/` — full list in `index.md`.
- **[crypto-js] Insecure entropy source - Math.random()**  
  https://hackerone.com/reports/678989 · sev 4.8
- **Grammarly Keyboard for Android "Authorization Code with PKCE" flow implementation vulnerability that allows account takeover**  
  https://hackerone.com/reports/824931 · sev 6.5 · bounty $2,000
- **Predictable Random Number Generator**  
  https://hackerone.com/reports/504731

### Use of a Key Past its Expiration Date (3 reports)
Folder: `weakness/Use of a Key Past its Expiration Date/` — full list in `index.md`.
- **Expired SSL certificate**  
  https://hackerone.com/reports/220615 · bounty $100
- **In App purchase Hack**  
  https://hackerone.com/reports/218287 · bounty $400
- **OAuth2 Access Token and App Password Security Vulnerability**  
  https://hackerone.com/reports/343111 · sev 6.4 · bounty $400

### User Interface (UI) Misrepresentation of Critical Information (3 reports)
Folder: `weakness/User Interface (UI) Misrepresentation of Critical Information/` — full list in `index.md`.
- **Unsafe downloaded file execution**  
  https://hackerone.com/reports/633600 · bounty $250
- **Mailsploit: a sender spoofing bug in over 30 email clients**  
  https://hackerone.com/reports/295339 · sev 7.4
- **Content Spoofing/Text Injection in https://support.cs.money and JS file not minified and uglyfied which makes it clearly readable**  
  https://hackerone.com/reports/997198 · bounty $200

### Write-what-where Condition (3 reports)
Folder: `weakness/Write-what-where Condition/` — full list in `index.md`.
- **OP_SCALL in LHS of a OP_ASGN resulting in arbitrary memory write**  
  https://hackerone.com/reports/226200 · bounty $200
- **[steam client] Opening a specific steam:// url overwrites files at an arbitrary location**  
  https://hackerone.com/reports/667242 · sev 5.3 · bounty $750
- **Race condition на market.games.mail.ru**  
  https://hackerone.com/reports/317557 · bounty $1,000

### Buffer Under-read (2 reports)
Folder: `weakness/Buffer Under-read/` — full list in `index.md`.
- **Buffer can be readable through Debug on metrics.solana.com**  
  https://hackerone.com/reports/962832
- **controlled buffer under-read in pack_unpack_internal()**  
  https://hackerone.com/reports/298246 · sev 6.2 · bounty $500

### Execution with Unnecessary Privileges (2 reports)
Folder: `weakness/Execution with Unnecessary Privileges/` — full list in `index.md`.
- **One Click Code Execution via File**  
  https://hackerone.com/reports/822609 · sev 8
- **[H1-2006 2020]  "Swiss Cheese" design style leads to helping Mårten Mickos pay poor hackers**  
  https://hackerone.com/reports/890272

### Failure to Sanitize Special Elements into a Different Plane (Special Element Injection) (2 reports)
Folder: `weakness/Failure to Sanitize Special Elements into a Different Plane (Special Element Injection)/` — full list in `index.md`.
- **[api.zomato.com] Abusing LocalParams (city_id) to Inject SOLR query**  
  https://hackerone.com/reports/953203 · sev 3.7 · bounty $150
- **Profile bio at rockstar is accepting control characters**  
  https://hackerone.com/reports/214763 · bounty $350

### Improper Handling of Insufficient Permissions or Privileges (2 reports)
Folder: `weakness/Improper Handling of Insufficient Permissions or Privileges/` — full list in `index.md`.
- **Access to support tickets and payment history, impersonate razer support staff**  
  https://hackerone.com/reports/776110 · bounty $1,500
- **curl overwrites local file with -J option if file non-readable, but file writable.**  
  https://hackerone.com/reports/926638

### Improper Neutralization of HTTP Headers for Scripting Syntax (2 reports)
Folder: `weakness/Improper Neutralization of HTTP Headers for Scripting Syntax/` — full list in `index.md`.
- **Cache poisoning via X-Forwarded-Host in www.shopify.com/partners/blog**  
  https://hackerone.com/reports/977851 · sev 3.6 · bounty $1,000
- **Audit log validation**  
  https://hackerone.com/reports/296632

### Incorrect Calculation of Buffer Size (2 reports)
Folder: `weakness/Incorrect Calculation of Buffer Size/` — full list in `index.md`.
- **first name and last name restrictions bypass**  
  https://hackerone.com/reports/260468 · bounty $20
- **An integer overflow found in /lib/urlapi.c**  
  https://hackerone.com/reports/547630 · bounty $150

### Missing Authorization (2 reports)
Folder: `weakness/Missing Authorization/` — full list in `index.md`.
- **Missing authorization allows sales only user to record payment.**  
  https://hackerone.com/reports/919008 · bounty $250
- **Access token stealing.**  
  https://hackerone.com/reports/821896 · sev 8.1 · bounty $1,200

### Off-by-one Error (2 reports)
Folder: `weakness/Off-by-one Error/` — full list in `index.md`.
- **Subdomain Takeover due to unclaimed domain pointing to AWS**  
  https://hackerone.com/reports/317005 · bounty $150
- **Exim off-by-one RCE vulnerability**  
  https://hackerone.com/reports/322935 · bounty $1,500

### Use of Hard-coded Cryptographic Key (2 reports)
Folder: `weakness/Use of Hard-coded Cryptographic Key/` — full list in `index.md`.
- **`Cody trolled us all` h1-702 CTF write-up**  
  https://hackerone.com/reports/507148
- **Slack DTLS uses a private key that is in the public domain, which may lead to SRTP stream hijack**  
  https://hackerone.com/reports/531032 · sev 8.7 · bounty $2,000

### Use of Inherently Dangerous Function (2 reports)
Folder: `weakness/Use of Inherently Dangerous Function/` — full list in `index.md`.
- **Blind SSRF on https://labs.data.gov/dashboard/Campaign/json_status/ Endpoint**  
  https://hackerone.com/reports/895696 · sev 4.9 · bounty $300
- **URL Spoof / Brave Shield Bypass**  
  https://hackerone.com/reports/255991 · bounty $200

### XML Entity Expansion (2 reports)
Folder: `weakness/XML Entity Expansion/` — full list in `index.md`.
- **c3p0 may be exploited by a Billion Laughs Attack when loading XML configuration**  
  https://hackerone.com/reports/509315 · sev 6.2
- **Pippo XML Entity Expansion (Billion Laughs Attack)**  
  https://hackerone.com/reports/506791 · sev 8.3

### Embedded Malicious Code (1 reports)
Folder: `weakness/Embedded Malicious Code/` — full list in `index.md`.
- **flatmap-stream malicious package (distributed via the popular events-stream)**  
  https://hackerone.com/reports/450006 · sev 10

### Exposed Dangerous Method or Function (1 reports)
Folder: `weakness/Exposed Dangerous Method or Function/` — full list in `index.md`.
- **Open memory dump method leaking customer information ,secret keys , password , source code & admin accounts**  
  https://hackerone.com/reports/783360 · sev 10

### Improper Check or Handling of Exceptional Conditions (1 reports)
Folder: `weakness/Improper Check or Handling of Exceptional Conditions/` — full list in `index.md`.
- **Create any military unit in any age**  
  https://hackerone.com/reports/802636 · bounty $1,100

### Improper Export of Android Application Components (1 reports)
Folder: `weakness/Improper Export of Android Application Components/` — full list in `index.md`.
- **Launch Any Activity in MyMail App**  
  https://hackerone.com/reports/376618 · sev 6.9 · bounty $500

### Improper Handling of URL Encoding (Hex Encoding) (1 reports)
Folder: `weakness/Improper Handling of URL Encoding (Hex Encoding)/` — full list in `index.md`.
- **HTML injection in support.razer.com [IE only]**  
  https://hackerone.com/reports/826463 · bounty $250

### Improper Neutralization of Escape, Meta, or Control Sequences (1 reports)
Folder: `weakness/Improper Neutralization of Escape, Meta, or Control Sequences/` — full list in `index.md`.
- **Camo Image Proxy Bypass with CSS Escape Sequences**  
  https://hackerone.com/reports/745953 · bounty $250

### Improper Neutralization of Script-Related HTML Tags in a Web Page (Basic XSS) (1 reports)
Folder: `weakness/Improper Neutralization of Script-Related HTML Tags in a Web Page (Basic XSS)/` — full list in `index.md`.
- **[bugs.fuzzing-project.org] HTML Injection via 'custom_field_7[]' parameter in '/view_all_set.php'**  
  https://hackerone.com/reports/903869 · sev 6.5

### Insecure Temporary File (1 reports)
Folder: `weakness/Insecure Temporary File/` — full list in `index.md`.
- **UNRESTRICTED FILE UPLOAD AT chat.makerdao.com**  
  https://hackerone.com/reports/692360

### Key Exchange without Entity Authentication (1 reports)
Folder: `weakness/Key Exchange without Entity Authentication/` — full list in `index.md`.
- **Broken Authentication: A project addition request can be used multiple time for different users**  
  https://hackerone.com/reports/319480

### Reliance on Reverse DNS Resolution for a Security-Critical Action (1 reports)
Folder: `weakness/Reliance on Reverse DNS Resolution for a Security-Critical Action/` — full list in `index.md`.
- **Multiple Subdomain Takeovers: fly.staging.shipt.com, fly.us-west-2.staging.shipt.com, fly.us-east-1.staging.shipt.com**  
  https://hackerone.com/reports/576857 · bounty $900

### Reusing a Nonce, Key Pair in Encryption (1 reports)
Folder: `weakness/Reusing a Nonce, Key Pair in Encryption/` — full list in `index.md`.
- **Key Reinstallation Attacks: Breaking WPA2 by forcing nonce reuse**  
  https://hackerone.com/reports/286740 · sev 6.8 · bounty $25,000

### Unprotected Transport of Credentials (1 reports)
Folder: `weakness/Unprotected Transport of Credentials/` — full list in `index.md`.
- **Credientals Over GET method in plain Text**  
  https://hackerone.com/reports/490899

### Use of Externally-Controlled Format String (1 reports)
Folder: `weakness/Use of Externally-Controlled Format String/` — full list in `index.md`.
- **Format String Vulnerability in the EdgeSwitch restricted CLI**  
  https://hackerone.com/reports/311884 · sev 7.2 · bounty $1,500

### Use of Hard-coded Password (1 reports)
Folder: `weakness/Use of Hard-coded Password/` — full list in `index.md`.
- **hardcoded password stored in javascript of https://████.mil**  
  https://hackerone.com/reports/991718

### XML Injection (1 reports)
Folder: `weakness/XML Injection/` — full list in `index.md`.
- **SVG file upload leads to XML injection**  
  https://hackerone.com/reports/845832
