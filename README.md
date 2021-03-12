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
