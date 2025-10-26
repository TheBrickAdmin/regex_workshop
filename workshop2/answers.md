# Workshop 2 — Answers (collapsible & slow reveal)

## 1) Capture username and domain
<details><summary>Hint 1</summary>Split on `@` using two named groups.</details>
<details><summary>Hint 2</summary>Be liberal on username characters but stop at whitespace.</details>
<details><summary>Answer</summary>

```
(?P<user>[^@\s]+)@(?P<domain>[^\s]+)
```
PowerShell: `$Matches['user']`, `$Matches['domain']`  
Python: `m.group('user')`, `m.group('domain')`
</details>

## 2) ERROR not preceded by DEBUG
<details><summary>Hint 1</summary>Use a negative lookbehind or a negative lookahead over the whole line.</details>
<details><summary>Hint 2</summary>Lookbehind: fixed-width text like `DEBUG` is OK.</details>
<details><summary>Answer (two options)</summary>

Negative lookahead on line:
```
^(?!.*DEBUG).*ERROR.*
```

Or negative lookbehind just before ERROR:
```
(?<!DEBUG.*)ERROR
```
(Engine support varies for variable-length; prefer the lookahead solution.)
</details>

## 3) Version numbers vX.Y.Z
<details><summary>Hint</summary>Use groups for digits separated by dots, prefixed by `v`.</details>
<details><summary>Answer</summary>

```
\bv(\d+)\.(\d+)\.(\d+)\b
```
Named variant:
```
\bv(?P<major>\d+)\.(?P<minor>\d+)\.(?P<patch>\d+)\b
```
</details>

## 4) Text inside parentheses
<details><summary>Hint 1</summary>Use a capturing group that avoids matching `)`.</details>
<details><summary>Hint 2</summary>Make the inner part non-greedy.</details>
<details><summary>Answer</summary>

```
\(([^)]*?)\)
```
</details>

## 5) Named groups for dates
<details><summary>Hint</summary>Use `(?P<name>...)` or `(?<name>...)` depending on engine.</details>
<details><summary>Answer</summary>

Pattern:
```
(?P<day>\d{2})-(?P<month>\d{2})-(?P<year>\d{4})
```
PowerShell:
```powershell
'02-10-2025' -match '(?<day>\d{2})-(?<month>\d{2})-(?<year>\d{4})' | Out-Null
$Matches['month']
```
Python:
```py
m = re.search(r'(?P<day>\d{2})-(?P<month>\d{2})-(?P<year>\d{4})', text)
m.group('year')
```
</details>
