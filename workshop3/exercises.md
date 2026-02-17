# Workshop 3 — Real-World & Performance (Exercises)
Make sure you are in the workshop3 directory to make sure relative paths work correctly.

## Regex Syntax Recap

### Advanced Patterns
- `(...)` — capture group
- `(?:...)` — non-capturing group
- `\1`, `\2` — backreferences to captured groups
- `(?=...)` — positive lookahead
- `(?!...)` — negative lookahead

### Flags/Modifiers
- **Multiline:** `^` and `$` match line boundaries
  - Python: `re.MULTILINE` or inline `(?m)`
  - Bash: `grep -E` (default line-by-line) or `grep -Pz` for null-delimited multiline
  - PowerShell: `[System.Text.RegularExpressions.RegexOptions]::Multiline` or inline `(?m)`
- **Dotall/Singleline:** `.` matches newlines too
  - Python: `re.DOTALL` or inline `(?s)`
  - Bash: `grep -Pz` with PCRE or inline `(?s)` with `-P`
  - PowerShell: `[System.Text.RegularExpressions.RegexOptions]::Singleline` or inline `(?s)`
- **Case-insensitive:** ignore case when matching
  - Python: `re.IGNORECASE` or inline `(?i)`
  - Bash: `grep -i` or inline `(?i)` with `-P`
  - PowerShell: `[System.Text.RegularExpressions.RegexOptions]::IgnoreCase` or inline `(?i)` or `-match` operator is case-insensitive by default

### Character Classes
- `.` — any character except newline
- `\d` — digit 0–9
- `\w` — word char: letters, digits, _
- `\s` — whitespace
- `\b` — word boundary

### Quantifiers
- `?` — zero or one
- `*` — zero or more
- `+` — one or more
- `{n}` — exactly n
- `{n,}` — at least n
- `{n,m}` — between n and m

## 1. Find duplicated words
Find consecutive duplicate words (e.g., `the the`, `Error Error`).

File: `samples/duplicate_words.txt`

**Python:** Replace `YOUR_REGEX_HERE` with your pattern
```python
import re; content = open('samples/duplicate_words.txt', 'r').read(); duplicates = re.findall(r'YOUR_REGEX_HERE', content); print("\n".join(f"  {dup}" for dup in duplicates))
```

**Bash:** Replace `YOUR_REGEX_HERE` with your pattern
```bash
grep -oE 'YOUR_REGEX_HERE' samples/duplicate_words.txt
```

**PowerShell:** Replace `YOUR_REGEX_HERE` with your pattern
```powershell
$content = Get-Content 'samples/duplicate_words.txt' -Raw
$pattern = 'YOUR_REGEX_HERE'
$matches = [regex]::Matches($content, $pattern)
$matches | ForEach-Object { $_.Value }
```

## 2. Clean HTML tags but preserve text
Remove all HTML tags using regex for quick cleanup.

File: `samples/messy.html`

**Python:** Replace `YOUR_REGEX_HERE` with your pattern
```python
import re; content = open('samples/messy.html', 'r').read(); cleaned = re.sub(r'YOUR_REGEX_HERE', '', content); print(cleaned)
```

**Bash:** Replace `YOUR_REGEX_HERE` with your pattern
```bash
sed 's|YOUR_REGEX_HERE||g' samples/messy.html
```

**PowerShell:** Replace `YOUR_REGEX_HERE` with your pattern
```powershell
$content = Get-Content 'samples/messy.html' -Raw
$pattern = 'YOUR_REGEX_HERE'
$content -replace $pattern, ''
```

## 3. Validate IPv4 vs IPv6
Write two separate patterns: a pragmatic IPv4 and a pragmatic IPv6. Test them on sample text.

**Python IPv4:** Replace `YOUR_IPV4_REGEX_HERE` with your IPv4 pattern
```python
import re; test_text = "192.168.1.1 and 256.300.400.500 and 10.0.0.1"; ipv4_pattern = r'YOUR_IPV4_REGEX_HERE'; matches = re.findall(ipv4_pattern, test_text); print("IPv4 matches:", matches)
```

**Python IPv6:** Replace `YOUR_IPV6_REGEX_HERE` with your IPv6 pattern
```python
import re; test_text = "2001:0db8:85a3:0000:0000:8a2e:0370:7334 and ::1 and fe80::1"; ipv6_pattern = r'YOUR_IPV6_REGEX_HERE'; matches = re.findall(ipv6_pattern, test_text); print("IPv6 matches:", matches)
```

**Bash IPv4:** Replace `YOUR_IPV4_REGEX_HERE` with your pattern
```bash
echo "192.168.1.1 and 256.300.400.500 and 10.0.0.1" | grep -oE 'YOUR_IPV4_REGEX_HERE'
```

**PowerShell IPv4:** Replace `YOUR_IPV4_REGEX_HERE` with your pattern
```powershell
$testText = "192.168.1.1 and 256.300.400.500 and 10.0.0.1"
$pattern = 'YOUR_IPV4_REGEX_HERE'
[regex]::Matches($testText, $pattern).Value
```

## 4. Multiline block extract
Extract content between lines starting with `BEGIN` and `END` inclusively.

File: `samples/block.txt`

**Python:** Replace `YOUR_REGEX_HERE` with your pattern (hint: use `re.DOTALL`)
```python
import re; content = open('samples/block.txt', 'r').read(); blocks = re.findall(r'YOUR_REGEX_HERE', content, re.DOTALL); print("\n---\n".join(blocks))
```

**Bash:** Replace `YOUR_REGEX_HERE` with your pattern
```bash
grep -Pzo 'YOUR_REGEX_HERE' samples/block.txt
```

**PowerShell:** Replace `YOUR_REGEX_HERE` with your pattern
```powershell
$content = Get-Content 'samples/block.txt' -Raw
$pattern = 'YOUR_REGEX_HERE'
$matches = [regex]::Matches($content, $pattern, [System.Text.RegularExpressions.RegexOptions]::Singleline)
$matches | ForEach-Object { $_.Value }
```

## 5. Detect catastrophic backtracking
Test which pattern causes catastrophic backtracking. Identify the problematic pattern and explain why.

**Test Pattern 1:** `^(a+)+$`  
**Test Pattern 2:** `^a+$`

**Python Test Harness:** Replace `YOUR_PATTERN_HERE` with each pattern
```python
import re, time; test_string = "a" * 20 + "b"; pattern = r'YOUR_PATTERN_HERE'; start = time.time(); result = re.match(pattern, test_string); elapsed = time.time() - start; print(f"Pattern: {pattern}\nMatch: {result}\nTime: {elapsed:.6f}s")
```

**PowerShell Test Harness:** Replace `YOUR_PATTERN_HERE` with each pattern
```powershell
$testString = "a" * 20 + "b"
$pattern = 'YOUR_PATTERN_HERE'
$stopwatch = [System.Diagnostics.Stopwatch]::StartNew()
$match = $testString -match $pattern
$stopwatch.Stop()
Write-Host "Pattern: $pattern`nMatch: $match`nTime: $($stopwatch.Elapsed.TotalSeconds)s"
```
