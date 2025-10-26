# Workshop 3 — Real-World & Performance (Exercises)

1. **Find duplicated words** (e.g., `the the`, `Error Error`). File: `samples/duplicate_words.txt`.

2. **Clean HTML tags but preserve text**  
   Remove tags using a regex for quick cleanup. File: `samples/messy.html`.

3. **Validate IPv4 vs IPv6**  
   Write two separate patterns: a pragmatic IPv4 and a pragmatic IPv6. Explain trade-offs.

4. **Multiline block extract**  
   Extract content between lines starting with `BEGIN` and `END` inclusively. File: `samples/block.txt`.

5. **Detect catastrophic backtracking**  
   Identify which of the two patterns is prone to backtracking and explain why:
   - `^(a+)+$`
   - `^a+$`
