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
## Task 5
Command: `sed -E 's/^([0-9]{4}-[0-9]{2}-[0-9]{2}) [0-9:]+ ([A-Z]+) ([A-Z]+) .*/\1 \2 \3/' firewall.log | head -n 5`
Result: 
#Version 1.5
#Software: Microsoft Windows Firewall
#Time Format: local
#Fields: date time action protocol src-ip dst-ip src-port dst-port size
2018-05-25 FORWARD TCP
Explanation: Utilizes capture groups '()' to isolate the date, action, and protocol fields. The backreferences '\1', '\2', and '\3' are used in the substitution string to rebuild the line, discarding the remaining fields.
## Task 6
Command: `grep -E ' ACCEPT TCP [^ ]+ [^ ]+ [^ ]+ 80 [0-9]+$' firewall.log | wc -l`
Result: 93
Explanation: Combines literal field matching with positional reasoning. Matches 'ACCEPT' and 'TCP', skips intermediate fields using '[^ ]+' (any non-space character), validates destination port '80', and anchors the size field at the end.
## Task 7
Command: `grep -E ' [0-9]{4}-[0-9]{2}-[0-9]{2} 0[0-2]:[0-9]{2}:[0-9]{2}' firewall.log | wc -l`
Result: 0
Explanation: Uses a character-class range '0[0-2]' to filter the hour digit, effectively capturing times between 00:00:00 and 02:59:59. The regex is anchored to the time field following the date.