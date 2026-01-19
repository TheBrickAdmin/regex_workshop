# Workshop 1 — Regex Fundamentals Exercises
Make sure you are in the workshop1 directory to make sure relative paths work correctly.

## Regex Syntax Recap

### Character Classes
- `.` — any character except newline
- `\d` — digit 0–9
- `\D` — not digit
- `\w` — word char: letters, digits, _
- `\W` — not word char
- `\s` — whitespace
- `\S` — not whitespace

### Anchors
- `^` — start of string/line
- `$` — end of string/line
- `\b` — word boundary

### Character Sets
- `[a-z]` — lowercase letters
- `[A-Z]` — uppercase letters
- `[0-9]` — digits
- `[^abc]` — NOT a, b, or c

### Quantifiers
- `?` — zero or one
- `*` — zero or more
- `+` — one or more
- `{n}` — exactly n
- `{n,}` — at least n
- `{n,m}` — between n and m

### Greedy vs. Lazy
- Greedy: `".+"`
- Lazy: `".+?"`

### Anchor Examples
- `^ERROR` — line starts with ERROR
- `WARN$` — line ends with WARN

## 1. Extract all IPv4 addresses

File: `samples/server.log`

**Python:** Replace `YOUR_REGEX_HERE` with your pattern
```python
import re; content = open('samples/server.log', 'r').read(); ip_addresses = re.findall(r'YOUR_REGEX_HERE', content); print("\n".join(f"  {ip}" for ip in ip_addresses))
```

**Bash:** Replace `YOUR_REGEX_HERE` with your pattern
```bash
grep -oE 'YOUR_REGEX_HERE' samples/server.log
```

**PowerShell:** Replace `YOUR_REGEX_HERE` with your pattern
```powershell
$content = Get-Content 'samples/server.log' -Raw
$ipPattern = 'YOUR_REGEX_HERE'
$matches = [regex]::Matches($content, $ipPattern)
$matches | ForEach-Object { $_.Value }
```

## 2. Validate product codes
Match only valid codes: 3 uppercase letters, hyphen, 4 digits. Example valid: `ABC-1234`

File: `samples/products.txt`

**Python:** Replace `YOUR_REGEX_HERE` with your pattern
```python
import re; content = open('samples/products.txt', 'r').read(); valid_codes = re.findall(r'YOUR_REGEX_HERE', content); print("\n".join(f"  {code}" for code in valid_codes))
```

**Bash:** Replace `YOUR_REGEX_HERE` with your pattern
```bash
grep -oE 'YOUR_REGEX_HERE' samples/products.txt
```

**PowerShell:** Replace `YOUR_REGEX_HERE` with your pattern
```powershell
$content = Get-Content 'samples/products.txt' -Raw
$pattern = 'YOUR_REGEX_HERE'
$matches = [regex]::Matches($content, $pattern)
$matches | ForEach-Object { $_.Value }
```

## 3. Remove all comments from config files
Delete lines starting with `#`

File: `samples/config.ini`

**Python:** Replace `YOUR_REGEX_HERE` with your pattern
```python
import re; content = open('samples/config.ini', 'r').read(); cleaned_content = re.sub(r'YOUR_REGEX_HERE', '', content); print(cleaned_content)
```

**Bash:** Replace `YOUR_REGEX_HERE` with your pattern
```bash
grep -v 'YOUR_REGEX_HERE' samples/config.ini
```

**PowerShell:** Replace `YOUR_REGEX_HERE` with your pattern
```powershell
$content = Get-Content 'samples/config.ini'
$content | Where-Object { $_ -notmatch 'YOUR_REGEX_HERE' }
```

## 4. Convert date format
From `DD/MM/YYYY` to `YYYY-MM-DD`. Perform a regex-based replacement.

File: `samples/dates.txt`

**Python:** Replace `YOUR_REGEX_HERE` with your pattern and `YOUR_REPLACEMENT_HERE` with your replacement
```python
import re; content = open('samples/dates.txt', 'r').read(); converted = re.sub(r'YOUR_REGEX_HERE', r'YOUR_REPLACEMENT_HERE', content); print(converted)
```

**Bash:** Replace `YOUR_REGEX_HERE` with your pattern and `YOUR_REPLACEMENT_HERE` with your replacement
```bash
sed 's|YOUR_REGEX_HERE|YOUR_REPLACEMENT_HERE|g' samples/dates.txt
```

**PowerShell:** Replace `YOUR_REGEX_HERE` with your pattern and `YOUR_REPLACEMENT_HERE` with your replacement
```powershell
$content = Get-Content 'samples/dates.txt' -Raw
$pattern = 'YOUR_REGEX_HERE'; $replacement = 'YOUR_REPLACEMENT_HERE'
$content -replace $pattern, $replacement
```

## 5. Match filenames ending in `.log`
Find only log filenames

File: `samples/server.log`

**Python:** Replace `YOUR_REGEX_HERE` with your pattern
```python
import re; content = open('samples/server.log', 'r').read(); log_files = re.findall(r'YOUR_REGEX_HERE', content); print("\n".join(f"  {file}" for file in log_files))
```

**Bash:** Replace `YOUR_REGEX_HERE` with your pattern
```bash
grep -oE 'YOUR_REGEX_HERE' samples/server.log
```

**PowerShell:** Replace `YOUR_REGEX_HERE` with your pattern
```powershell
$logPattern = 'YOUR_REGEX_HERE'
(Select-String -Path 'samples/server.log' -Pattern $logPattern -AllMatches).Matches.Value
```
