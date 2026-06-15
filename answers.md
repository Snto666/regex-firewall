## Task 1
Command: `grep -c -v '^#' firewall.log`
Result: 100000
Explanation: Uses the '-c' flag for counting matches and '-v' to invert the search. The anchor '^#' ensures the regex matches only lines beginning with a hash character, effectively excluding the 4-line metadata header.
## Task 2
Command: `grep -E ' (DROP|REJECT) ' firewall.log | wc -l`
Result: 60156
Explanation: Employs an extended regex (-E) with the alternation operator '|' inside a capturing group. Anchoring the search with spaces ensures we match the 'action' field exclusively, preventing false positives from other fields.
