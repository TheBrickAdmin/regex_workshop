# Workshop 1 — Answers (collapsible & slow reveal)

## 1) Extract IPv4
<details><summary>Hint 1</summary>Match digits separated by dots.</details>
<details><summary>Hint 2</summary>Use `{1,3}` for each segment with grouping.</details>
<details><summary>Answer</summary>

**Regex Pattern:**
```
\b(\d{1,3}\.){3}\d{1,3}\b
```

**Python:**
```python
# One-liner to support REPL:
import re; content = open('samples/server.log', 'r').read(); ip_addresses = re.findall(r'\b(?:\d{1,3}\.){3}\d{1,3}\b', content); print("\n".join(f"  {ip}" for ip in ip_addresses))
```

**Bash:**
```bash
# Extract IPv4 addresses using grep
grep -oE '\b([0-9]{1,3}\.){3}[0-9]{1,3}\b' samples/server.log
```

**PowerShell:**
```powershell
# Extract IPv4 addresses from server.log
$content = Get-Content 'samples/server.log' -Raw
$ipPattern = '\b(\d{1,3}\.){3}\d{1,3}\b'
$matches = [regex]::Matches($content, $ipPattern)
$matches | ForEach-Object { $_.Value }
```
</details>

## 2) Validate product codes
<details><summary>Hint</summary>Uppercase character class, exact counts, anchors.</details>
<details><summary>Answer</summary>

**Regex Pattern:**
```
[A-Z]{3}-\d{4}
```

**Python:**
```python
# One-liner to support REPL:
import re; content = open('samples/products.txt', 'r').read(); valid_codes = re.findall(r'[A-Z]{3}-\d{4}', content); print("\n".join(f"  {code}" for code in valid_codes))
```

**Bash:**
```bash
# Show valid product codes
grep -oE '[A-Z]{3}-[0-9]{4}' samples/products.txt
```

**PowerShell:**
```powershell
# Extract valid product codes
$content = Get-Content 'samples/products.txt' -Raw
$pattern = '[A-Z]{3}-\d{4}'
$matches = [regex]::Matches($content, $pattern)
$matches | ForEach-Object { $_.Value }
```
</details>

## 3) Remove comment lines
<details><summary>Hint</summary>Use start-of-line anchor in multiline mode.</details>
<details><summary>Answer</summary>

**Regex Pattern:**
```
(?m)^#.*$
```

**Python:**
```python
# One-liner to support REPL:
import re; content = open('samples/config.ini', 'r').read(); cleaned_content = re.sub(r'(?m)^#.*$\n?', '', content);print(cleaned_content)
```

**Bash:**
```bash
# Remove comment lines
grep -v '^#' samples/config.ini
```

**PowerShell:**
```powershell
# Remove comment lines
$content = Get-Content 'samples/config.ini'
$content | Where-Object { $_ -notmatch '^#' }
```
</details>

## 4) Convert DD/MM/YYYY → YYYY-MM-DD
<details><summary>Hint</summary>Capture day, month, year and reorder in replacement.</details>
<details><summary>Answer</summary>

**Regex Pattern:**
```
(\d{2})\/(\d{2})\/(\d{4})
```

**Python:**
```python
# One-liner to support REPL:
import re; content = open('samples/dates.txt', 'r').read(); converted = re.sub(r'(\d{2})\/(\d{2})\/(\d{4})', r'\3-\2-\1', content); print(converted)
```

**Bash:**
```bash
# Convert date format using sed
sed 's|\([0-9]\{2\}\)/\([0-9]\{2\}\)/\([0-9]\{4\}\)|\3-\2-\1|g' samples/dates.txt
```

**PowerShell:**
```powershell
# Convert date format
$content = Get-Content 'samples/dates.txt' -Raw
$pattern = '(\d{2})\/(\d{2})\/(\d{4})'; $replacement = '$3-$2-$1'
$content -replace $pattern, $replacement
```
</details>

## 5) Match `.log` files
<details><summary>Hint</summary>Escape the dot and anchor the end.</details>
<details><summary>Answer</summary>

**Regex Pattern:**
```
\.log$
```

**Python:**
```python
# One-liner to support REPL:
import re; content = open('samples/server.log', 'r').read(); log_files = re.findall(r'\b\w+\.log\b', content); print("\n".join(f"  {file}" for file in log_files))
```

**Bash:**
```bash
# Find .log files
grep -oE '\b[a-zA-Z0-9_-]+\.log\b' samples/server.log
```

**PowerShell:**
```powershell
# Find .log files
$logPattern = '\b\w+\.log\b'
(Select-String -Path 'samples/server.log' -Pattern $logPattern -AllMatches).Matches.Value
```
</details>
