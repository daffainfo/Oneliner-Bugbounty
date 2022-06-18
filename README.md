# Oneliner-Bugbounty
A collection  oneliner scripts for bug bounty

### Auto scanner

```bash
subfinder -d site.com -all | naabu | httpx | nuclei -t nuclei-templates
```

### Finding files (For example in here .json file)

```bash
subfinder -d site.com -all | naabu | httpx | waybackurls | grep -E ".json(?:onp?)?$"
```

### Find interesting subdomain (For example like admin.staging.example.com) 

```bash
subfinder -d site.com -all | dnsprobe -silent | cut -d ' ' -f1 | grep --color 'dmz\|api\|staging\|env\|v1\|stag\|prod\|dev\|stg\|test\|demo\|pre\|admin\|beta\|vpn\|cdn\|coll\|sandbox\|qa\|intra\|extra\|s3\|external\|back'
```

### Find SQL injection at scale

```bash
subfinder -d site.com -all -silent | waybackurls | sort -u | gf sqli > gf_sqli.txt; sqlmap -m gf_sqli.txt --batch --risk 3 --random-agent | tee -a sqli.txt
```

### Find open redirects at scale

```bash
subfinder -d site.com -all -silent | waybackurls | sort -u | gf redirect | qsreplace 'https://example.com' | httpx -fr -title --match-string 'Example Domain'
```

### Scanning top exploited vulnerabilities according to CISA

```bash
subfinder -d site.com -all -silent | httpx -silent | nuclei -rl 50 -c 15 -timeout 10 -tags cisa -vv
```

### Bruteforce subdomains

```bash
subfinder -d site.com -all -silent | httpx -silent | hakrawler | tr "[:punct:]" "\n" | sort -u > wordlist.txt

puredns bruteforce wordlist.txt site.com -r resolvers.txt -w output.txt
```

## References
- [ReconOne](https://twitter.com/ReconOne_/)