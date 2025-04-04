# Room: Subdomain Enumeration  
**Site:** [TryHackMe.com](https://tryhackme.com)  
**Type:** Walkthrough  
**Author:** Jerome Goldwin M.  
**Date:** 2025/04/04

Hello again. This is Jerome Goldwin.

Today I am going to learn about subdomain enumeration. Which is a process of finding what are the subdomain a domain has so that we can have a larger attack surface and try to discover more potential points of vulnerablity.

There are three types of subdomain enumeration methods: Brute Force, OSINT, and Virtual Host.

## OSINT - SSL/TLS Certificates

When a SSL/TLS ( Secure Socket Layer / Transport Layer Security ) certificate is created for a domain by the CA ( Certificate Authority ). The CA's take part in what is called "Certificate Transparency (CT) logs". These are publicly accessible and they do this because they want to stop malcious certificates and accidentally made certificates being used. I can use this to my advantage to find the no. of subdomain a domain have. This database is actually historical so we may find some old gems.

[Link: https://crt.sh/](https://crt.sh/)

## OSINT - Search Engines

I don't know that search engines can be used for these kind of purposes with the help of filter and I have been using it for years. I can search for the subdomain using the wildcard in the subdomain's place followed by the domain name and top level domain. For example, `site:*.google.com` would give me all the subdomain google have. If I don't want a subdomain to be displayed I can add the following along with it `-site:{subdomain}.google.com`, whereas you have replace `{subdomain}` with the name you want not to be displayed.

## DNS Bruteforce

Bruteforce DNS(Domain Name System) is as the name suggest bruteforce searching tens and hundreds and thousands of subdomain until we find results. I can use DNSrecon to do this action.

```bash
dnsrecon -t brt -d {domain}.{TLD}
```

The `-t` flag is for the type of reconnaissance we are doing, in this case bruteforce. `-d` is the domain name.

This is new, we are dealing with a new method.

## OSINT - Sublist3r

Sublist3r is a domain enumeration tool which is fast and is automated so there is an automated method I guess. Yes when used, it revealed that it searches for match in the databases that are publicly available. Very useful tool.

```bash
sublist3r -d {domain}.{TLD}
```

Next and final stop.

## Virtual Hosts

See I already know that not every webpages are not openly available even they use the `robots.txt` to hide some webpages from being displayed in a search engine's results. So there is also a similar case with subdomain. So they have all the subdomains in a list DNS server which I can attack. When I say attack it is not a bad thing. Just reconnaissance. Hate the game not the player.

It is usually also recorded on the developer's machines in the location `/etc/hosts` file if it is Linux or `c:windowssystem32driversetchosts` if it is Windows that will map domain names with their IP address.

I can manipulate the Host header and monitor the response to see if I discovered a new website.

I can also autmate this process by using a wordlist of commonly used subdomains.

```bash
fuff -w {path_to_wordlist} -H "Host: FUZZ.{domain}.{tld}" -u {url}
```

`-w` switch is for the specification of the wordlist file. `-H` switch is for manipulating the HOST header in the HTTP request, finally `-u` switch is the specification of the url.

This will return any valid result but we don't want that. I have to filter the large files. So we can use a `-fs` switch which will let me filter it by size of the reply.

```bash
fuff -w {path_to_wordlist} -H "Host: FUZZ.{domain}.{TLD}" -u {url} -fs {size}
```
And we are done.
