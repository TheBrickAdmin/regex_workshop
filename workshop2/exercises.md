# Workshop 2 — Groups, Alternation, Lookarounds (Exercises)

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

### Groups and Capturing
- `(abc)` — Capturing Group
- `(?P<name>abc)` — Named Capturing Group (Python)
- `(?<name>abc)` — Named Capturing Group (.NET/PowerShell)
- `(?:abc)` — Non-capturing group

### Alternation
- `cat|dog` — match "cat" OR "dog"

### Lookarounds
- `(?=abc)` — Lookahead: match if followed by "abc"
- `(?!abc)` — Negative lookahead: match if NOT followed by "abc"
- `(?<=abc)` — Lookbehind: match if preceded by "abc"
- `(?<!abc)` — Negative lookbehind: match if NOT preceded by "abc"

1. **Capture username and domain from email addresses**  
   File: `samples/emails.txt`. Use named groups where possible.

2. **Select log lines with ERROR not preceded by DEBUG**  
   File: `samples/mixed-logs.txt`.

3. **Match version numbers** in the form `vX.Y.Z` where X,Y,Z are integers.  
   File: `samples/versions.txt`.

4. **Extract only the text inside parentheses** from arbitrary strings.  
   Input: lines in `samples/mixed-logs.txt` that contain parentheses.

5. **Capture date components** `DD-MM-YYYY` using named groups `day`, `month`, `year`.  
   Show how to access them in PowerShell and Python.
