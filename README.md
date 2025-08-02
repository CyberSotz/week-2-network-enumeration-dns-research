# 🔍 Advanced Reconnaissance with `whois`, `dig`, and `whatweb` in Kali Linux
**Week 2 Research Report**
**By: Muhammad Naveed Ul Hassan**


## 📌 Introduction
In the reconnaissance phase of cybersecurity assessments or penetration tests, understanding the target’s digital footprint is critical. This week, I explored **three essential tools** in Kali Linux: `whois`, `dig`, and `whatweb`. Each serves a unique purpose in **information gathering**, from domain ownership to DNS structure to web technologies in use. Here’s a breakdown of what they do, how they work internally, and how they relate to each other in practice.

## 1️⃣ `whois` – Domain Registration and Ownership Lookup
### 🛠️ What It Does
`whois` retrieves **domain registration information** from publicly accessible WHOIS databases. It is commonly used to obtain:
- Registrant's contact details (unless privacy-protected)
- Registrar information
- Domain creation/expiration dates
- Nameservers
- WHOIS server chain referrals

### ⚙️ How It Works
- Uses the **WHOIS protocol** over **TCP port 43**
- Sends a plain-text query to a WHOIS server (e.g., `whois.iana.org`, `whois.verisign-grs.com`)
- If the queried WHOIS server is a registry (e.g., Verisign for `.com`), it often refers the request to the specific registrar’s WHOIS server

### 🔐 Privacy Notes
Due to GDPR and registrar-specific policies, many domains now hide contact information using WHOIS privacy services.

### 🧪 Example
```bash
whois example.com
```

### 📚 Real-World Use Cases
- OSINT in Red Team operations
- Identifying ownership of malicious/phishing domains
- Legal investigations or domain dispute resolution
- Detecting newly registered or suspicious domains

## 2️⃣ `dig` – DNS Record Enumeration and Analysis
### 🛠️ What It Does
`dig` (Domain Information Groper) is a powerful tool for querying **Domain Name System (DNS)** records. It allows you to investigate:
- A, AAAA (IPv6), MX, TXT, NS, SOA, CNAME records
- TTLs, authorities, and response time
- DNS resolution paths (recursive vs authoritative)

### ⚙️ How It Works
- Sends a DNS query using **UDP (default)** or **TCP** on **port 53**
- Can target specific DNS resolvers (e.g., Google DNS: `8.8.8.8`)
- Provides detailed response breakdown

### 🧪 Example
```bash
dig example.com
dig @8.8.8.8 example.com MX +noall +answer
dig -x 93.184.216.34
```

### 📚 Real-World Use Cases
- Enumerating DNS infrastructure
- Identifying misconfigured DNS (e.g., zone transfers)
- Subdomain mapping
- Detecting DNS poisoning or cache manipulation

## 3️⃣ `whatweb` – Website Technology Fingerprinting
### 🛠️ What It Does
`whatweb` is a passive-to-active **web reconnaissance tool** used to fingerprint:
- Web servers (Apache, Nginx)
- CMS platforms (WordPress, Drupal, Joomla)
- Programming frameworks
- SSL cert info, headers, meta tags, JavaScript files, and more

### ⚙️ How It Works
- Sends HTTP(S) requests to the target URL
- Analyzes headers, HTML body, JS files, cookies
- Uses plugin-based detection engine (~1700 plugins)

### 🧪 Example
```bash
whatweb example.com
whatweb -v -a 3 -l output.txt example.com
```

### 📚 Real-World Use Cases
- Identifying attack surfaces
- Mapping third-party libraries and tech stack
- Finding analytics, CDNs, or load balancers

## 🔄 Tool Comparison Table

| Feature            | `whois`                        | `dig`                             | `whatweb`                           |
|-------------------|---------------------------------|-----------------------------------|-------------------------------------|
| **Main Focus**     | Domain registration info        | DNS resolution and structure      | Website technology fingerprinting   |
| **Protocol**       | WHOIS (TCP port 43)             | DNS (UDP/TCP port 53)             | HTTP/HTTPS (TCP port 80/443)        |
| **Data Collected** | Registrar, dates, contacts      | IPs, DNS records, TTL, authority  | Server, CMS, plugins, headers       |
| **Active/Passive** | Passive                         | Semi-active                       | Active (can be stealthy with flags) |
| **Ideal For**      | Legal, OSINT, threat analysis   | Infra discovery, DNS analysis     | Reconnaissance, web stack detection |

## 🚀 My Key Takeaways
- These tools build the **foundation of external recon**, and each covers a **distinct layer of information**.
- `whois` for legal and ownership footprint
- `dig` for network-level DNS mapping
- `whatweb` for application-level insights

## 🗂️ Next Steps
- Combine these tools in automated recon scripts
- Compare results with tools like `theHarvester`, `sublist3r`, and `dnsrecon`
- Go deeper into passive vs active reconnaissance strategies
