# 🕵️‍♂️ Content Discovery - TryHackMe Walkthrough  

**Room:** Content Discovery  
**Site:** [TryHackMe](https://tryhackme.com/)  
**Type:** Walkthrough  
**Author:** Jerome Goldwin M.  
**Date:** 2025/04/02  

## 🔎 Introduction  
Hello again. This is **Jerome Goldwin**, and I am about to hack one more room—**Content Discovery**. This challenge explores how hidden elements in a web page can be found and exploited.  

I've started my **victim machine** and my **attackbox**. Let's dive in.  

---

## 🛠️ Three Ways of Discovering Hidden Content  
1. **Manual Discovery**  
2. **Automated Discovery**  
3. **OSINT (Open Source Intelligence)**  

### 📌 OSINT - Open Source Intelligence  
OSINT involves gathering publicly available data to analyze for security risks.  

- The **robots.txt** file can reveal restricted areas that should not be indexed by search engines, but still exist and are publicly accessible.  
- **Favicons** can sometimes identify which framework a website is using, helping us find vulnerabilities.  
- **Sitemap.xml** reveals website structure and sometimes exposes sensitive areas.  
- **HTTP headers** provide information about the server, framework, and technologies in use.  
- **Framework stack** comments in HTML or source code can reveal important details about the website's tech stack.  

### 🕵️‍♂️ OSINT - Google Hacking/Dorking  
Google search operators (such as `site:`, `inurl:`, `filetype:`) help refine searches and find sensitive information that shouldn't be public.  

- More details: [Google Hacking Wikipedia](https://en.wikipedia.org/wiki/Google_hacking)  

### 🔧 OSINT - Wappalyzer  
- A tool that identifies **frameworks, CMS, and technologies** used by a website.  
- Available as an **online tool** and a **browser extension**.  

### 🕰️ OSINT - Wayback Machine  
- An archive that stores past versions of websites.  
- Useful for uncovering outdated and vulnerable pages.  
- [Wayback Machine](https://archive.org/web/)  

### ☁️ OSINT - S3 Buckets  
- **Amazon S3** stores files and static websites, but misconfigured permissions can expose sensitive data.  
- The common format for bucket URLs:  https://{name}.s3.amazonaws.com
- Can be found in **source code, robots.txt, debug logs, GitHub repositories, and automated scans**.  

---

## ⚙️ Automated Content Discovery  
Automation speeds up the process of discovering hidden content.  

### 📂 Wordlists  
Wordlists contain predefined words to test for hidden directories and files.  
- Example: [SecLists by Daniel Miessler](https://github.com/danielmiessler/SecLists)  

### 🔍 Automated Tools  
- **ffuf** - Uses "FUZZ" in the URL to replace with words from a wordlist.  
- **dirb** - Appends words from a wordlist to a URL to check for accessible directories.  
- **gobuster** - Directory and file enumeration tool.  

### 🔥 Execution Example  
Using `ffuf` to find hidden directories:  
```bash
ffuf -u https://target-site.com/FUZZ -w /usr/share/wordlists/common.txt
```

## 🎯 Key Takeaways
- Manual, Automated, and OSINT techniques can reveal sensitive data.

- robots.txt, sitemap.xml, HTTP headers, and frameworks can expose vulnerabilities.

- Google Dorking, Wappalyzer, Wayback Machine, GitHub searches, and S3 buckets provide valuable OSINT insights.

- Automation tools like ffuf, dirb, and gobuster speed up content discovery.
