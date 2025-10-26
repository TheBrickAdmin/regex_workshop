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
import re

# Read and extract IPv4 addresses from server.log
with open('samples/server.log', 'r') as file:
    content = file.read()
    
ip_addresses = re.findall(r'\b(\d{1,3}\.){3}\d{1,3}\b', content)
for ip in ip_addresses:
    print(ip)

# Alternative with validation (proper IPv4 range 0-255)
ip_pattern = r'\b(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\b'
valid_ips = re.findall(ip_pattern, content)
```

**Bash:**
```bash
# Extract IPv4 addresses using grep
grep -oE '\b([0-9]{1,3}\.){3}[0-9]{1,3}\b' samples/server.log

# Alternative using sed
sed -n 's/.*\b\([0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\)\b.*/\1/p' samples/server.log
```

**PowerShell:**
```powershell
# Extract IPv4 addresses from server.log
$content = Get-Content 'samples/server.log' -Raw
$ipPattern = '\b(\d{1,3}\.){3}\d{1,3}\b'
$matches = [regex]::Matches($content, $ipPattern)
$matches | ForEach-Object { $_.Value }

# Alternative one-liner
Select-String -Path 'samples/server.log' -Pattern '\b(\d{1,3}\.){3}\d{1,3}\b' -AllMatches | 
    ForEach-Object { $_.Matches } | ForEach-Object { $_.Value }
```
</details>

## 2) Validate product codes
<details><summary>Hint</summary>Uppercase character class, exact counts, anchors.</details>
<details><summary>Answer</summary>

**Regex Pattern:**
```
^[A-Z]{3}-\d{4}$
```

**Python:**
```python
import re

# Read product codes and validate
with open('samples/products.txt', 'r') as file:
    lines = file.readlines()

pattern = r'^[A-Z]{3}-\d{4}$'
valid_codes = []
invalid_codes = []

for line in lines:
    code = line.strip()
    if re.match(pattern, code):
        valid_codes.append(code)
        print(f"✓ Valid: {code}")
    else:
        invalid_codes.append(code)
        print(f"✗ Invalid: {code}")

print(f"\nValid codes: {len(valid_codes)}")
print(f"Invalid codes: {len(invalid_codes)}")
```

**Bash:**
```bash
# Validate product codes using grep
echo "Valid product codes:"
grep -E '^[A-Z]{3}-[0-9]{4}$' samples/products.txt

echo -e "\nInvalid product codes:"
grep -vE '^[A-Z]{3}-[0-9]{4}$' samples/products.txt

# Count valid vs invalid
valid_count=$(grep -cE '^[A-Z]{3}-[0-9]{4}$' samples/products.txt)
total_count=$(wc -l < samples/products.txt)
invalid_count=$((total_count - valid_count))
echo -e "\nValid: $valid_count, Invalid: $invalid_count"
```

**PowerShell:**
```powershell
# Read and validate product codes
$codes = Get-Content 'samples/products.txt'
$pattern = '^[A-Z]{3}-\d{4}$'

$results = $codes | ForEach-Object {
    $isValid = $_ -match $pattern
    [PSCustomObject]@{
        Code = $_
        Valid = $isValid
        Status = if ($isValid) { "✓ Valid" } else { "✗ Invalid" }
    }
}

$results | ForEach-Object { Write-Host "$($_.Status): $($_.Code)" }

$validCount = ($results | Where-Object { $_.Valid }).Count
$invalidCount = ($results | Where-Object { -not $_.Valid }).Count
Write-Host "`nValid: $validCount, Invalid: $invalidCount"
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
import re

# Read config file and remove comment lines
with open('samples/config.ini', 'r') as file:
    content = file.read()

# Remove lines starting with #
cleaned_content = re.sub(r'(?m)^#.*$\n?', '', content)
print("Original content:")
print(content)
print("\nCleaned content:")
print(cleaned_content)

# Alternative: process line by line
with open('samples/config.ini', 'r') as file:
    lines = file.readlines()

non_comment_lines = [line for line in lines if not line.strip().startswith('#')]
print("\nNon-comment lines:")
print(''.join(non_comment_lines))
```

**Bash:**
```bash
# Remove comment lines using grep
echo "Original file:"
cat samples/config.ini

echo -e "\nWithout comments (using grep):"
grep -v '^#' samples/config.ini

echo -e "\nWithout comments (using sed):"
sed '/^#/d' samples/config.ini

# Save to new file
grep -v '^#' samples/config.ini > samples/config_no_comments.ini
```

**PowerShell:**
```powershell
# Read and remove comment lines
$content = Get-Content 'samples/config.ini'

Write-Host "Original content:"
$content | ForEach-Object { Write-Host $_ }

Write-Host "`nWithout comments:"
$filteredContent = $content | Where-Object { $_ -notmatch '^#' }
$filteredContent | ForEach-Object { Write-Host $_ }

# Using regex replacement on entire content
$fullContent = Get-Content 'samples/config.ini' -Raw
$cleanedContent = $fullContent -replace '(?m)^#.*$\r?\n?', ''
Write-Host "`nUsing regex replacement:"
Write-Host $cleanedContent
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
import re

# Sample dates to convert
sample_dates = [
    "25/12/2023",
    "01/01/2024",
    "15/08/2022",
    "Today is 26/10/2025 and tomorrow is 27/10/2025"
]

pattern = r'(\d{2})\/(\d{2})\/(\d{4})'
replacement = r'\3-\2-\1'

for text in sample_dates:
    converted = re.sub(pattern, replacement, text)
    print(f"Original: {text}")
    print(f"Converted: {converted}")
    print()

# Find all dates and convert them
text = "Meeting on 15/03/2024, deadline 20/04/2024"
dates = re.findall(pattern, text)
print("Found dates (day, month, year):")
for day, month, year in dates:
    print(f"{day}/{month}/{year} → {year}-{month}-{day}")
```

**Bash:**
```bash
# Convert date format using sed
echo "Sample dates:"
echo "25/12/2023"
echo "01/01/2024" 
echo "15/08/2022"

echo -e "\nConverted dates:"
echo "25/12/2023" | sed 's|\([0-9]\{2\}\)/\([0-9]\{2\}\)/\([0-9]\{4\}\)|\3-\2-\1|g'
echo "01/01/2024" | sed 's|\([0-9]\{2\}\)/\([0-9]\{2\}\)/\([0-9]\{4\}\)|\3-\2-\1|g'
echo "15/08/2022" | sed 's|\([0-9]\{2\}\)/\([0-9]\{2\}\)/\([0-9]\{4\}\)|\3-\2-\1|g'

# Process multiple dates in text
echo -e "\nConverting text with multiple dates:"
echo "Meeting on 15/03/2024, deadline 20/04/2024" | \
    sed 's|\([0-9]\{2\}\)/\([0-9]\{2\}\)/\([0-9]\{4\}\)|\3-\2-\1|g'

# Using grep to find dates first
echo -e "\nFinding dates with grep:"
echo "Meeting on 15/03/2024, deadline 20/04/2024" | \
    grep -oE '[0-9]{2}/[0-9]{2}/[0-9]{4}'
```

**PowerShell:**
```powershell
# Convert date format
$sampleDates = @(
    "25/12/2023",
    "01/01/2024", 
    "15/08/2022",
    "Meeting on 15/03/2024, deadline 20/04/2024"
)

$pattern = '(\d{2})\/(\d{2})\/(\d{4})'
$replacement = '$3-$2-$1'

Write-Host "Date conversion examples:"
foreach ($text in $sampleDates) {
    $converted = $text -replace $pattern, $replacement
    Write-Host "Original:  $text"
    Write-Host "Converted: $converted"
    Write-Host ""
}

# Extract and convert dates
$text = "Meeting on 15/03/2024, deadline 20/04/2024"
$matches = [regex]::Matches($text, $pattern)
Write-Host "Found dates:"
foreach ($match in $matches) {
    $day = $match.Groups[1].Value
    $month = $match.Groups[2].Value
    $year = $match.Groups[3].Value
    Write-Host "$day/$month/$year → $year-$month-$day"
}
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
import re

# Read server.log and find .log filenames
with open('samples/server.log', 'r') as file:
    content = file.read()

# Pattern to match .log files
log_pattern = r'\b\w+\.log\b'
log_files = re.findall(log_pattern, content)

print("Found .log files:")
for log_file in log_files:
    print(f"  {log_file}")

# More specific pattern for various log file patterns
advanced_pattern = r'\b[a-zA-Z0-9_-]+\.log\b'
advanced_matches = re.findall(advanced_pattern, content)
print(f"\nWith advanced pattern: {advanced_matches}")

# Find lines containing .log files
lines_with_logs = []
with open('samples/server.log', 'r') as file:
    for line_num, line in enumerate(file, 1):
        if re.search(r'\.log', line):
            lines_with_logs.append((line_num, line.strip()))

print("\nLines containing .log references:")
for line_num, line in lines_with_logs:
    print(f"Line {line_num}: {line}")
```

**Bash:**
```bash
# Find .log files using grep
echo "Finding .log files in server.log:"
grep -oE '\b[a-zA-Z0-9_-]+\.log\b' samples/server.log

echo -e "\nLines containing .log:"
grep '\.log' samples/server.log

echo -e "\nWith line numbers:"
grep -n '\.log' samples/server.log

# Using different approaches
echo -e "\nUsing awk to extract .log files:"
awk '{
    while (match($0, /[a-zA-Z0-9_-]+\.log/)) {
        print substr($0, RSTART, RLENGTH)
        $0 = substr($0, RSTART + RLENGTH)
    }
}' samples/server.log

# Find unique .log files
echo -e "\nUnique .log files:"
grep -oE '\b[a-zA-Z0-9_-]+\.log\b' samples/server.log | sort | uniq
```

**PowerShell:**
```powershell
# Find .log files in server.log
$content = Get-Content 'samples/server.log'

Write-Host "Finding .log files:"
$logPattern = '\b\w+\.log\b'
$matches = Select-String -Path 'samples/server.log' -Pattern $logPattern -AllMatches
$logFiles = $matches | ForEach-Object { $_.Matches } | ForEach-Object { $_.Value }
$logFiles | ForEach-Object { Write-Host "  $_" }

Write-Host "`nLines containing .log:"
$content | ForEach-Object { 
    if ($_ -match '\.log') { 
        Write-Host $_ 
    } 
}

Write-Host "`nWith line numbers:"
$content | ForEach-Object -Begin { $i = 1 } -Process { 
    if ($_ -match '\.log') { 
        Write-Host "Line $i : $_" 
    }
    $i++
}

# Extract all .log filenames using regex
Write-Host "`nAll .log files found:"
$allMatches = [regex]::Matches($content -join "`n", '\b[a-zA-Z0-9_-]+\.log\b')
$uniqueLogFiles = $allMatches | ForEach-Object { $_.Value } | Sort-Object -Unique
$uniqueLogFiles | ForEach-Object { Write-Host "  $_" }
```
</details>
