## Task 1
Command: `grep -c -v '^#' firewall.log`
Result: 100000
Explanation: Uses the '-c' flag for counting matches and '-v' to invert the search. The anchor '^#' ensures the regex matches only lines beginning with a hash character, effectively excluding the 4-line metadata header.
## Task 2
Command: `grep -E ' (DROP|REJECT) ' firewall.log | wc -l`
Result: 60156
Explanation: Employs an extended regex (-E) with the alternation operator '|' inside a capturing group. Anchoring the search with spaces ensures we match the 'action' field exclusively, preventing false positives from other fields.
## Task 3
Command: `grep -E ' [A-Z]+ [A-Z]+ 11\.' firewall.log | wc -l`
Result: 33217
Explanation: Matches the source IP field by identifying the preceding action and protocol fields. The dot ('.') is escaped as '\.' to force a literal match, ensuring we target the 11. subnet specifically, rather than any character.
## Task 4
Command: `grep -E ' [0-9]{7}$' firewall.log | wc -l`
Result: 2343
Explanation: Targets the size field using the quantifier '{7}' to match exactly seven digits. The end-of-line anchor '$' ensures the match is strictly the size field, avoiding accidental matches with port numbers.