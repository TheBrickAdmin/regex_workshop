# Workshop 1 — Answers (collapsible & slow reveal)

## 1) Extract IPv4
<details><summary>Hint 1</summary>Match digits separated by dots.</details>
<details><summary>Hint 2</summary>Use `{1,3}` for each segment with grouping.</details>
<details><summary>Answer</summary>

```
\b(\d{1,3}\.){3}\d{1,3}\b
```
</details>

## 2) Validate product codes
<details><summary>Hint</summary>Uppercase character class, exact counts, anchors.</details>
<details><summary>Answer</summary>

```
^[A-Z]{3}-\d{4}$
```
</details>

## 3) Remove comment lines
<details><summary>Hint</summary>Use start-of-line anchor in multiline mode.</details>
<details><summary>Answer</summary>

```
(?m)^#.*$
```
</details>

## 4) Convert DD/MM/YYYY → YYYY-MM-DD
<details><summary>Hint</summary>Capture day, month, year and reorder in replacement.</details>
<details><summary>Answer</summary>

Pattern:
```
(\d{2})\/(\d{2})\/(\d{4})
```
Replacement (PowerShell):
```
-replace '(\d{2})\/(\d{2})\/(\d{4})', '$3-$2-$1'
```
Python:
```py
re.sub(r'(\d{2})\/(\d{2})\/(\d{4})', r'\3-\2-\1', text)
```
</details>

## 5) Match `.log` files
<details><summary>Hint</summary>Escape the dot and anchor the end.</details>
<details><summary>Answer</summary>

```
\.log$
```
</details>
