# Web-Hunter: Automated Web Vulnerability Scanner

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Kali Linux](https://img.shields.io/badge/Platform-Kali_Linux-red?logo=linux)
![License](https://img.shields.io/badge/License-MIT-green)

Web-Hunter is a modular, command-line tool developed to streamline the process of discovering critical web application vulnerabilities. It integrates powerful security tools into a unified Python-based scanner for offensive security testing.

---

## 🔍 Key Features

- **Automated Scans for:**
  - SQL Injection (SQLi)
  - Cross-Site Scripting (XSS)
  - Cross-Site Request Forgery (CSRF)

- **Target Audience:** Penetration testers, ethical hackers, and cybersecurity professionals.
- **Modes:** Choose from individual or combined scan options.

---

## ⚙️ Technology Stack

- **Language:** Python 3.x  
- **Platform:** Kali Linux (recommended due to built-in security tools)

### Integrated Tools:
- [`SQLmap`](https://sqlmap.org): Detects and exploits SQL injection vulnerabilities.
- [`Wfuzz`](https://github.com/xmendez/wfuzz): Used for fuzzing and XSS detection.
- [`XSRFProbe`](https://github.com/0xInfection/XSRFProbe): Identifies CSRF weaknesses.

### Python Dependencies:
- `subprocess`, `argparse`, `os`

> Ensure all tools are installed on your system using:
```bash
sudo apt update && sudo apt install sqlmap wfuzz xsrfprobe
```

---

## 🧱 System Architecture

- **Input Handler:** Accepts and validates target URL input.
- **Execution Layer:** Interfaces with external tools via `subprocess`.
- **Output Parser:** Extracts and formats scan results for readability.

### 🔄 Workflow:
1. User enters a target URL.
2. Selects scan type (SQLi, XSS, CSRF, or All).
3. Web-Hunter runs the appropriate tool(s).
4. Displays findings in a readable format (plaintext or JSON).

---

## 🛠️ Tool Integration & Code Example

Python communicates with CLI tools using subprocess:

```python
import subprocess

def run_sqlmap(url):
    command = f"sqlmap -u {url} --batch"
    process = subprocess.Popen(command.split(), stdout=subprocess.PIPE)
    output, _ = process.communicate()
    return output.decode()
```

Includes:
- Exception handling (invalid input, missing tools)
- Logging for failed runs
- Output parsing using regex or keyword matching

---

## 📊 Vulnerability Scans

### SQLi (SQL Injection)
```bash
sqlmap -u http://example.com --batch
```

### XSS (Cross-Site Scripting)
```bash
wfuzz -c -z file,payloads/xss.txt -d "param=FUZZ" http://example.com
```

### CSRF (Cross-Site Request Forgery)
```bash
xsrfprobe -u http://example.com
```

---

## 🧪 Testing Strategy

- **Unit Tests:** Validate input, check subprocess calls.
- **Integration Tests:** Scanned against test environments like DVWA & OWASP Juice Shop.
- **Performance Metrics:** SQLi scans complete in ~2–5 minutes depending on response size and complexity.

---

## ⚠️ Limitations

- Relies on external tools (sqlmap, wfuzz, xsrfprobe).
- Accuracy depends on the performance of integrated tools (may return false positives/negatives).
- Currently focuses only on SQLi, XSS, and CSRF (does not cover full OWASP Top 10).

---

## 🚀 Future Roadmap

- GUI version using Tkinter or web dashboard
- Add scans for server misconfigurations (e.g., via Nikto)
- HTML/PDF report generation with findings and remediation

---

## 🧭 Getting Started

### 🔧 Prerequisites:
- Linux OS (Kali preferred)
- Python 3.x installed
- Required tools:
```bash
sudo apt install sqlmap wfuzz xsrfprobe
```

### 📥 Installation:
```bash
git clone <repository-url>
cd Web-Hunter
python3 web_hunter.py
```

### ▶️ Usage:
```text
Enter target URL: http://example.com
Select scan type: 
1. SQLi 
2. XSS 
3. CSRF 
4. All
```

---

## 📄 License

MIT © [Your Name]
