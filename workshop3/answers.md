# Workshop 3 — Answers (collapsible & slow reveal)

## 1) Duplicated words
<details><summary>Hint</summary>Think backreference to the same word boundary-to-boundary.</details>
<details><summary>Answer</summary>

```
\b(\w+)\s+\1\b
```
</details>

## 2) Strip HTML tags (quick-and-dirty)
<details><summary>Hint</summary>Match `<` followed by anything not `>` until `>`.</details>
<details><summary>Answer</summary>

```
<[^>]+>
```
Note: For robust HTML parsing use a proper parser, not regex.
</details>

## 3) IPv4 vs IPv6 (pragmatic)
<details><summary>Hint</summary>Start simple; do not overfit edge-cases.</details>
<details><summary>Answer</summary>

IPv4 (simple, not range-perfect):
```
\b(\d{1,3}\.){3}\d{1,3}\b
```
IPv6 (compressed forms tolerated, pragmatic):
```
\b[0-9A-Fa-f:]{2,}\b
```
Discussion: strict validation becomes complex; prefer parsing libraries in production.
</details>

## 4) Multiline block extract
<details><summary>Hint</summary>Use DOTALL (singleline) to make `.` match newlines.</details>
<details><summary>Answer</summary>

```
(?s)BEGIN.*?END
```
Non-greedy `.*?` ensures the shortest block.
</details>

## 5) Catastrophic backtracking
<details><summary>Hint</summary>Nested quantifiers are suspicious.</details>
<details><summary>Answer</summary>

`^(a+)+$` is prone to catastrophic backtracking due to nested `+`.  
`^a+$` is linear-time.
</details>
